# Location name tooltip enhancement to the Fairycode module on the Runescape wiki

Fairy rings are circles of mushrooms, at specific locations in the world, used in the game for teleportation. Each fairy ring has a 3 letter code, as an address. You dial a code from any fairy ring to be teleported to the ring that corresponds to the entered code.

As they are a frequently used transportation method in the game, wiki articles often mention a fairy code. The wiki has a template for formatting these codes to give them a style that stands out in the page. 

Sometimes, a fairy code is mentioned on an article, but it isn't exactly clear where the corresponding fairy ring is located. I decided I would update the template to add a tooltip that would show the official location name for that fairy code. 

The template's functionality was provided by a Lua module that prepared the HTML code to put in the page. This page shows the changes I made to the module: [version diff for my edits](https://oldschool.runescape.wiki/?title=Module:Fairycode&diff=15094353&oldid=14437836)&#8203;<sup>([archive.today&nbsp;copy](http://archive.today/9VFLi))</sup>

To start, I encoded a mapping from the fairy codes to the corresponding location names as key-value pairs. In Lua, this is implemented with the table type. I wrote the mapping in the syntax for a table literal and assigned this to a variable in the module.

The original output was a `<span>` element which used CSS to style the three letters it contained, so my first version was to add the location as a `title` attribute to that element.

This change caused a problem with another template. There was a map of the world which labeled the locations of the fairy rings with their fairy code, however, the output of this template was being used as arguments to the `Map` template. Special characters in the `Fairycode` template's output were causing syntax bugs when inserted into the arguments of the call. I replaced special characters in my output with the HTML escape-sequences and made a function to process the location name, escaping any special characters, before outputting. It then worked as expected.

The improvment was working; hovering the mouse cursor over a fairy code showed a tooltip with the location name. However, the approach of using the `title` attribute had some issues: 
1. There was no visual indication that the extra information was there.
2. I read that using the `title` attribute in this way isn't accessible to assistive technologies.

Instead of using the `title` attribute, I put the original `<span>` element inside an `<abbr>` element. This allowed the issues to be addressed:
1. There is visual indication by a dotted underline and, when pointing at it, the cursor has a question mark attached.
2. I set the `aira-label` text such that assistive technologies will read out both the fairy code and the location name.

*Created using intellectual property belonging to Jagex Limited under the terms of [Jagex's Fan Content Policy](https://legal.jagex.com/docs/policies/fan-content-policy).
This content is not endorsed by or affiliated with Jagex.*
