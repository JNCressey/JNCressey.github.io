# Attempt to document the AI scripting language and configurable game constants in Tzar: The Burden of the Crown

There is a choice of AIs to assign to a each player when setting up a game. For human players, this AI will operate when the player turns on AI assistance.

I found the AIs are programmable in a relatively text-based language. I found some information in the manual about creating custom scenarios, but did not find a complete documentation for this AI script.

I found I could add additional AIs by adding additional script files to the folder where the original AIs were stored. Some files had the file extension `AI` while others had `AIS`. The scripts with `AIS` were able to include other AI files, this is the method of code re-use, since a common AI file that handles the basics could be included in multiple AIs that implement more specific stratergies.

The main jist of an AI script is a list of commands that tell the AI a goal of how much of a unit, building, resource, or tehnologies to get. examples:

    rule have 2 farms end
    rule have 10 cows end

Comments are preceded by a semicolon. Anything after a semicolon won't be processed as AI rules. example:

    ;------- make cavalries
    rule have 10 heavy_cavalry end ;this comment is after a rule
    ;rule have 2 barracks end ;this rule is commened out, so will be ignored
    

I found that quantities could be plain numbers or a percentage. I think the percentage would be the percentage of the population limit. Although I'm not sure if it's of the current population capacity with your houses or the total poopulation limit that's set for the game.

    rule have 40% peons end
    rule have 10 footman end


From looking at the examples, the most basic logic control I found was that a rule can contain a condition. examples:
    
    rule when peons 10 have 2 barracks end
    rule when barracks 2 have 5 maceman end
  
I also found a rule can stop the inclusion of following rules until it is satisfied by putting the word `critial` before it. In the following example, the AI will aim for 2 farms and 20 peasants (and any other following commands) only after it has 5 cows. It appears that frequently used critical rules are ones that only contain a condition, or ones that only contain an objective.

    critical rule when cows 5 end ;only contains a condition. the rule does not tell the AI to aim for anything, it only blocks the following commands until the condition is met
    rule have 20 peons end
    critical rule have barracks end ;only contains an objective. it acts both as an aim to get a barracks, and it blocks the following commands until it's done
    rule have 10 footman end
  
I also found some control in the form of curly brace blocks. It appears that if a command within a block stops the following commands, it only stops the followong commands in the block. Commands that come after the block continue to be acted upon. In the following example, the aim for 2 farms is blocked until it has 5 cows, but the aim for 10 footmen isn't blocked.

    { critical rule when cows 5 end
      rule have 2 farms end
    }
    rule have 10 footman end

From a commented out rule (`;rule say "hmai talk on" forget this end`), I found that the AI can say a message in the game chat, this helped with interrogating how commands are run. For the player to see what is said, the cheat `hmai talk on` has to be submitted, which the AI can say itself. I also found another part of a rule command is `forget this`. This makes it so the rule is only done once. The following example will do the talk-enabling cheat once, and then say "hello world" every time the script is processed, which appears to be every 5 or so seconds.

    rule say "hmai talk on" forget this end
    rule say "hello world" end

From using the say command, I determined that every 5 or so seconds, the script runs from the top and the result of the run commands updates the AI's goals.

Rule with larger demands appeared to be treated as higher priority by the AI. To tame the priority, rules could be split up to require a smaller quantity at each time - requiring larger quantities only after the smaller quantity is reached. example:

    rule when footman 10 have 20 footman end
    rule when footman 20 have 50 footman end

## unit names

By looking at the configurable game constants for attack bonuses and language localisation, I found the coded names for the different units and buildings, and these can be used in the arguments for the AI scripts.

There was a file that allowed configuring the prices and base stats of units and buildings. The data was aranged as tab-separated-values.

There was a file for configuring the unit class bonuses. There was a line for each category and an associated list of units in that group

## more complex control

I found some rules with a variety of different things that can be testest for. and I found that triggers can be set and read.

    rule when civ european, cathedral trigger Path1_Religion end ;tests that the civ is european and has a cathedral. sets the trigger Path1_Religion
    
    { critical rule when not trigger Path1 end ;tests against the trigger Path1
    ...
    }
    
    rule when not trigger Path1, random 40% trigger Path1_War, Path1 end ;test for the trigger Path1 and a random test with 40% chance of being true

    { critical rule when difficulty hard, food 15000 end ;test for the game difficulty to be hard, and having an amount of the food resource
    ...
    }

I also found the AI can use the travern resource conversion. Although, the script can only request to have `convert` and not specify which resources are being convered. It appears that the actual AI playing the game makes the decision of what to convert, and the script can have some influence over the conversion by chosing *when* to do it based on having amounts of resources.

    { critical rule when difficulty hard, food 15000 end
      critical rule have tavern end
      { critical rule when not gold 10000 end
        rule say "Converting food to gold" end
        rule have 500 convert end
      }
    }
