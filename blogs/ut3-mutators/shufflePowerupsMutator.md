# Intro 

The computer game "Unreal Tournament 3" has a system for small modifications to be selected when you start a game. It calls these small mods "mutators". I made a mutator that introduces some randomness to a game by shuffling the various powerups at the start of a match.

# How It Works

The game engine provides a way to run some code from the mutator whenever an actor (i.e. a game object) is spawned for the game, by implementing the method `CheckReplacement(Actor other)`. This allows the mutator to spawn a replacement and prevent the original from appearing in game.

At the start of a game, the pickup factories for the game’s power-ups are spawned, these are locations in the map that regularly create the power-ups. My mutator’s implementation of `CheckReplacement` checks if the spawned actor is a pickup factory for a power-up and, if it is, replaces it with a different pickup factory according to a permutation.

The pickup factories weren’t meant to be allowed to be dynamically spawned so have a few values set in their class that prevents it. (I think the reason is that it effects lighting graphics and might cause desynchonised behaviour in multiplayer.) In the package for my mutator, I made small classes that extend each type of pickup factory and overwrite those values – these can then be spawned by the mutator when it does the replacement.

The permutation that controls the replacements is regularly reshuffled.

# Configuration Options

A mutator is able to load values from a configuration file that is easily edited in a text editor. For this I provided options that allow different groups of powerups (timed powerups, the big health and shield pickups, and the single-use special weapons) to be included in the shuffle, and options to shuffle them all together or as separate groups.

I also provided an option to choose the frequency for reshuffling the permutation that controls the replacements.

# Reusing the Permutation 

In order for the same permutation to be used over multiple games, it is also saved to the configuration file after it's generated.

I wanted to keep the shuffle as consistent as possible when the options are changed but the reshuffle frequency indicates that a reshuffle isn’t desired. So, I implemented the permutation in a structure that defines a shuffle for all the power-ups together, and allows for derivation of permutations with stricter configurations. The stricter permutation keeps the replacements that are still valid, and uses pairs of invalid assignments to make new valid replacements.

# Reshuffle Frequency

In order to have the effect of the permutation being reshuffled at the specified frequency, the mutator checks at the beginning of the match whether a shuffle is due and, if it is, performs the reshuffling. The game engine provides the event `PreBeginPlay` which runs before each match and runs before any of the `CheckReplacement` calls.

- If the frequency is every match, that is easily implemented by treating the shuffle always as being due.

- If the frequency is every session (this is each time a new game is started from the menu but continuing through back-to-back matches), then a check that the game-time is small will tell if a shuffle is due, because that starts at 0 at the beginning of the session, but does not reset each match.

- For monthly, daily, and hourly, I saved the previous shuffle date in the configuration file. Then checking whether a shuffle is due is easily determined by checking equality of part of the date, because the date is provided as a string including the date parts and time of day.

- I also provided 7 weekly options: "every Sunday", "every Monday", etc. Again, comparing to the saved value for the previous shuffle date, I determine whether the specified weekday has started since the previous shuffle. To do this, I translate the dates into an integer on an absolute scale, and use modular arithmetic to determine how much to subtract from the current date to find the start of the current week (according to the specified weekday being the start of weeks) - then the shuffle is due if the last shuffle date's absolute number is less than for the start of the week.

# Modulo Operator (%) Bug

When shuffling using the built-in `Rand` function, I was getting the same sequence every time. I wanted to set the random seed but ensure that I wasn’t altering a global random number generator used by other parts of the game, so I implemented a random number generator in the mutator.

I used the modulo operator (%) to produce a random number within a range from the PRNG state. However I found a bug that it was often producing the wrong answer. I suspected that the modulo operator was converting the PRNG state into a float and losing precision, so I implemented a modulo function that calculated it correctly.

