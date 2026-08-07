<div style="color:darkred">this blog is not complete yet, still to finish writing up</div>

<script type="module" src="./assets/interactive-generator.js"></script>

<link rel="stylesheet" href="./assets/interactive-generator.css">

# Cistercian Numerals Minecraft Banners

My repo: [https://github.com/JNCressey/Cistercian-Numerals-Minecraft-Banners](https://github.com/JNCressey/Cistercian-Numerals-Minecraft-Banners)

## Intro

Cistercian numerals are symbols that can represent the numbers 1-9999, invented by Cistercian monks in the early 13th century. 

This Numberphile video explains how they work: [Youtube: 
The Forgotten Number System - Numberphile](https://www.youtube.com/watch?v=9p55Qgt7Ciw)

They act as a compact version of base-10, with the four corners of the glyph representing the four digits. The order of the digits is like a backwards "Z" pattern with the top-right corner representing the units place. 

<details open>
	<summary>The form of each digit</summary>
	<!-- todo alt text -->
	<img src="./examples/cistercian-numeral-forms.png" alt="">
</details>

<details open>
	<summary>Some examples of Cistercian numerals</summary>
	<!-- todo alt text -->
	<img src="./examples/cistercian-numerals.png" alt="">
</details>

The compact design of the numerals can be useful in Minecraft. Usually, one way of showing numbers in Minecraft is to use banners, with one Arabic numeral per banner.

I designed a set of banner patterns that resemble a half of a Cistercian numeral, which allows two banners to represent a Cistercian numeral which is equivellent to four base-10 digits.

<details open>
	<summary>Some examples of my Minecraft banners designs</summary>
	<!-- todo alt text -->
	<img src="./examples/my-banners.png" alt="">
</details>



## Web-Browser Based Interactive Generator

I made a webpage that can generate the required banner patterns for an input number. I programmed it by writing javascript modules.

There is a core module which generates the data of the required sequence of banner patterns. I made this follow the below flowchart by splitting it into methods.
- I labelled each point of the main flowchart where flow converges.
	- From each, I wrote a method that starts at the labelled point and performs the actions and branching of the flowchart. But when it reaches another labelled point, it returns with a call for the corresponding next method.
- I made a method that implements the auxiliary flowchart, that the other main methods can use as an action for the relevant nodes of the flowchart.

I wrote a module that draws the result of what the Cistercian numeral is supposed to look like. It draws it on a canvas element. To draw each digit, I made a method that can be given an origin and set of directions so that it draws the digit with the correct rotation/reflection and position. It draws the digit by defining a square of four points and connecting the required points acording to the digit's face value.

I wrote a module that draws a preview of the banner on a canvas element. It iterates over the sequence of banner patterns, provided by the other module, and calls a function that draws that pattern step.


	<div id="generatorWidget">
		<h2>Interactive Generator</h2>
		
		<noscript>
			<p>The interactive generator requires Javascript enabled to work. Showing an example output instead.</p>
		</noscript>
		
		<form id="generatorForm">
			<label for="numberInput">Number Input:</label>
			<input id="numberInput" name="numberInput" type="number" required min="0" max="9999" value="2026" disabled>
			<script>document.getElementById("numberInput").value="";</script>
			<br>
			
			<label> Background Colour:</label>
			<select id="backgroundColor" name="backgroundColor" required disabled>
				<noscript><option value="white">White</option></noscript>
			</select>
			<br>
			
			<label>Foreground Colour:</label>
			<select id="foregroundColor" name="foregroundColor" required disabled>
				<noscript><option value="black" >Black</option></noscript>
			</select>
			<br>
			
			<button type="submit" disabled>Generate banner patterns</button>
		</form>
		<script>document.querySelectorAll('#generatorForm :disabled').forEach((el)=>{ el.disabled = false; });</script>
		
		<p>The following output shows what the selected Cistercian numeral is supposed to look like. The two banners are a representation of the left and right sides of the numeral.</p>
		
		<p>The command may be too long for chat, so you might need to use a command block.</p>
		
		<h3 id="outputNumeralHeading">Output<noscript>: for 2026</noscript></h3>
		
		<details open>
			<summary>The cistercian numeral</summary>
			<div class="numeralBorder">
				<canvas id="cistercianNumeralOutput" width="200" height="400">
					<img src="./assets/noscript/cistercianNumeral-2026.png">
				</canvas>
			</div>
		</details>
		
		
		<div id="outputSides">
			<div id="outputSectionLeft">
				<h4 class="bannerSideHeading">Left Banner<noscript>: 2020</noscript></h3>
				
				<details open>
					<summary> Banner preview</summary>
					<div class="previewBorder">
						<canvas id="bannerPreviewLeft" class="bannerPreview" width="200" height="400">
							<img src="./assets/noscript/cistercianBanner-2026-left.png">
						</canvas>
					</div>
				</details>
				
				<h5>Give command</h5>
				<textarea id="giveCommandLeft" class="giveCommand">/give @p minecraft:white_banner[banner_patterns=[{pattern:half_horizontal,color:black},{pattern:stripe_top,color:white},{pattern:half_horizontal_bottom,color:black},{pattern:stripe_bottom,color:white},{pattern:stripe_middle,color:white},{pattern:stripe_right,color:black}]] 1</textarea>
				<script>document.getElementById("giveCommandLeft").value="";</script>
				<br>
				
				<button id="copyCommandLeft" class="copyCommandButton" disabled>Copy Command</button>
				<script>document.getElementById("copyCommandLeft").disabled = false;</script>
				
				<h5>Crafting/Loom steps</h5>
				<div class="craftingList">
					<table>
						<noscript>
							<tr><th>Start.</th>
								<td>White Banner</td>
								<td><img src="./assets/icons/white-banner.png"></td>
								<td></td>
								<td></td>
							</tr>
							<tr><th>Step 1.</th>
								<td>Black Dye</td>
								<td><img src="./assets/icons/black-dye.png"></td>
								<td>Per Fess</td>
								<td><img src="./assets/icons/per-fess.png"></td>
							</tr>
							<tr><th>Step 2.</th>
								<td>White Dye</td>
								<td><img src="./assets/icons/white-dye.png"></td>
								<td>Chief</td>
								<td><img src="./assets/icons/chief.png"></td>
							</tr>
							<tr><th>Step 3.</th>
								<td>Black Dye</td>
								<td><img src="./assets/icons/black-dye.png"></td>
								<td>Per Fess Inverted</td>
								<td><img src="./assets/icons/per-fess-inverted.png"></td>
							</tr>
							<tr><th>Step 4.</th>
								<td>White Dye</td>
								<td><img src="./assets/icons/white-dye.png"></td>
								<td>Base</td>
								<td><img src="./assets/icons/base.png"></td>
							</tr>
							<tr><th>Step 5.</th>
								<td>White Dye</td>
								<td><img src="./assets/icons/white-dye.png"></td>
								<td>Fess</td>
								<td><img src="./assets/icons/fess.png"></td>
							</tr>
							<tr><th>Step 6.</th>
								<td>Black Dye</td>
								<td><img src="./assets/icons/black-dye.png"></td>
								<td>Pale Sinister</td>
								<td><img src="./assets/icons/pale-sinister.png"></td>
							</tr>
						</noscript>
					</table>
				</div>
			</div>
			
			<div id="outputSectionRight">
				<h4 class="bannerSideHeading">Right Banner<noscript>: 6</noscript></h3>
				
				<details open>
					<summary> Banner preview</summary>
					<div class="previewBorder">
						<canvas id="bannerPreviewRight" class="bannerPreview" width="200" height="400">
							<img src="./assets/noscript/cistercianBanner-2026-right.png">
						</canvas>
					</div>
				</details>
				
				<h5>Give command</h5>
				<textarea id="giveCommandRight" class="giveCommand">/give @p minecraft:white_banner[banner_patterns=[{pattern:stripe_right,color:black},{pattern:half_horizontal_bottom,color:white},{pattern:stripe_middle,color:white},{pattern:stripe_left,color:black}]] 1</textarea>
				<script>document.getElementById("giveCommandRight").value="";</script>
				<br>
				
				<button id="copyCommandRight" class="copyCommandButton" disabled>Copy Command</button>
				<script>document.getElementById("copyCommandRight").disabled = false;</script>
				
				
				<h5>Crafting/Loom steps</h5>
				<div class="craftingList">
					<table>
						<noscript>
							<tr><th>Start.</th>
								<td>White Banner</td>
								<td><img src="./assets/icons/white-banner.png"></td>
								<td></td>
								<td></td>
							</tr>
							<tr><th>Step 1.</th>
								<td>Black Dye</td>
								<td><img src="./assets/icons/black-dye.png"></td>
								<td>Pale Sinister</td>
								<td><img src="./assets/icons/pale-sinister.png"></td>
							</tr>
							<tr><th>Step 2.</th>
								<td>White Dye</td>
								<td><img src="./assets/icons/white-dye.png"></td>
								<td>Per Fess Inverted</td>
								<td><img src="./assets/icons/per-fess-inverted.png"></td>
							</tr>
							<tr><th>Step 3.</th>
								<td>White Dye</td>
								<td><img src="./assets/icons/white-dye.png"></td>
								<td>Fess</td>
								<td><img src="./assets/icons/fess.png"></td>
							</tr>
							<tr><th>Step 4.</th>
								<td>Black Dye</td>
								<td><img src="./assets/icons/black-dye.png"></td>
								<td>Pale Dexter</td>
								<td><img src="./assets/icons/pale-dexter.png"></td>
							</tr>
						</noscript>
					</table>
				</div>
			</div>
		</div>
	</div>


## Flowchart

I made a flowchart so that a player can follow it as crafting instructions, without using the interactive generator, with just the flowchart images as references.

To use the flow chart, you first need to decide the digits you will make:

1. Choose a side of the numeral to make:
	- the hundreds and units
	- or the thousands and tens.
2. Choose two digits. Call them digit A and digit B.<br>With A being the larger digit, from their digit values, ignoring place value. (eg, for both 2080 and 8020: A=8 and B=2.)


Start at the top of the main flowchart.

When the main flowchart tells you to use the auxiliary flowchart, follow the steps on the other image for the single digit that the main flowchart told you to use. Then return to the main flowchart where you left from.

<details>
	<summary> Main flowchart </summary>
	<!-- todo alt text -->
	<img alt="Main flowchart" src="./flowcharts/cistercian-numerals-main.png">
</details>

<details>
	<summary> Auxiliary flowchart </summary>
	<!-- todo alt text -->
	<img alt="Auxiliary flowchart" src="./flowcharts/cistercian-numerals-auxiliary.png">
</details>


I used UMLet to draw the flowcharts.

---

*Minecraft is a trademark of Mojang/Microsoft. This site is not affiliated with or endorsed by Mojang or Microsoft.*
