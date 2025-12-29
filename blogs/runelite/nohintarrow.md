# Plugin for RuneLite: No Hint-Arrow

I made an accessibility-focused plugin for the RuneLite client, a client for the game RuneScape.

In the game, when there are tutorials or something the game wants to point to, it produces a flashing yellow arrow.
I saw some people complain about this in relation to their epilepsy.

I decided I would make a plugin to help.
I had not made a RuneLite plugin before, but I saw that the plugins are programmed using Java and was confident with my familiarity with the language.

## Minimum Viable Product

To start, the instructions to begin making a plugin is to clone the example plugin project which also comes with function that runs the game with your plugin available for testing. I followed the instructions to replace the example properties with descriptions of my plugin.

From looking at the code for a plugin that was complained about for producing the same flashing yellow arrow, I had found that the arrow is called a 'hint arrow'.
I checked the API docs for RuneLite to find a method to remove the hint-arrow, along with some other methods to interrogate the current state of the arrow.

I started by adding a call to clear the hint-arrow in the function that is run every game tick. And, when testing it, the hint-arrow was successfully removed from the tutorial.

## Delay to remove
## Substite marker
## Debugging features
## Not working with mage training arena plugin==
