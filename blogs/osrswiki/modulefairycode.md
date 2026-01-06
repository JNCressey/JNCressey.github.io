# Location name tooltip enhancement to the Fairycode module on the Runescape wiki

Fairy rings are circles of mushrooms, at specific locations in the world, used in the game for teleportation. Each fairy ring has a 3 letter code, as an address. You dial a code from any fairy ring to be teleported to the ring that corresponds to the entered code.

As they are a frequently used transportation method in the game, wiki articles often mention a fairy code. The wiki has a template for formatting these codes to give them a style that stands out in the page. 

Sometimes, a fairy code is mentioned on an article, but it isn't exactly clear where the corresponding fairy ring is located. I decided I would update the template to add a tooltip that would show the official location name for that fairy code. 

The template's functionality was provided by a Lua module that prepared the HTML code to put in the page. This page shows the changes I made to the module: [version diff for my edits](https://oldschool.runescape.wiki/?title=Module:Fairycode&diff=15094353&oldid=14437836)&#8203;<sup>([archive.today&nbsp;copy](http://archive.today/9VFLi))</sup>

To start, I encoded a mapping from the fairy codes to the corresponding location names as key-value pairs. In Lua, this is implemented with the table type. I wrote the mapping in the syntax for a table literal and assigned this to a variable in the module.

The original output was a `<span>` node containing the stylised code, so my first version was to add the location as a `title` attribute to that node. This worked when hovering the mouse cursor over a fairy code. However, this approach had some issues: 
1. There was no visual indication that the extra information was there.
2. I read that using the `title` attribute in this way isn't accessible to assistive technologies.

Instead of using the title attribute, now, the original styled `<span>` node is put within an `<abbr>` node. This allowed the issues to be addressed:
1. There is a visual indication by a dotted underline and the cursor has a question mark when pointing at the node.
2. The `aira-label` text is set for assistive technologies to read out both the fairy code and the location name.

Finally, there were a few complications that I fixed: 
* The output was erroneous when the template was passed a fairy code that had no location defined. The template needed to work with such fairy codes because, sometimes, a fairy code without a location is used within a combination code. I made the module simply return the original version of the stylised `<span>` node when a location name wasn't defined. This also has the benefit of being a safe fallback when a new fairy code is added to the game and is mentioned in an article before the location name is added to the module.
* The output of this template was also passed into the arguments of other templates for using it as labels, but the output now was inserting special characters that would break the other template calls. I replaced special characters in my output with their HTML escape-sequence and made a function to process the location name, escaping any special characters, before outputting.


*Created using intellectual property belonging to Jagex Limited under the terms of [Jagex's Fan Content Policy](https://legal.jagex.com/docs/policies/fan-content-policy).
This content is not endorsed by or affiliated with Jagex.*
