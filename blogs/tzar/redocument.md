# Attempt to document the AI scripting language and configurable game constants in Tzar: The Burden of the Crown

There is a choice of AIs to assign to a each player when setting up a game. For human players, this AI will operate when the player turns on AI assistance.

I found the AIs are programmable in a relatively text-based language. I found some information in the manual about creating custom scenarios, but did not find a complete documentation for this AI script.

I found I could add additional AIs by adding additional script files to the folder where the original AIs were stored.

The main jist of an AI script is a list of commands that tell the AI a goal of how much of a unit, building, or resource to get.

From looking at the examples, I found there is some kind of logic control where a command can stop the inclusion of following commands until it is completed.

I also found some control in the form of curly brace blocks. It appears that if a command within a block stops the following commands, it only stops the followong commands in the block. Commands that come after the block continue to be acted upon.

I found a command to say a message in the game chat, this helped with interrogating how commands are run.

From using the say command at the beginning of the script, I determined that every 5 or so seconds, the script runs from the top and the result of the run commands updates the AI's goals.

By looking at the configurable game constants for attack bonuses and language localisation, I found the coded names for the different units and buildings, and these can be used in the arguments for the AI scripts.

There was a file that allowed configuring the prices and base stats of units and buildings. The data was aranged as tab-separated-values.

There was a file for configuring the unit class bonuses. There was a line for each category and an associated list of units in that group
