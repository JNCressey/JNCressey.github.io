
<script>
  const toggle = document.getElementById("theme-toggle");
  const stored = localStorage.getItem("theme");

  if (stored) {
    document.documentElement.setAttribute("data-theme", stored);
  }

  toggle.addEventListener("click", () => {
    const current = document.documentElement.getAttribute("data-theme");
    const next = current === "dark" ? "light" : "dark";
    document.documentElement.setAttribute("data-theme", next);
    localStorage.setItem("theme", next);
  });
</script>

<button id="theme-toggle">Toggle theme</button>

GitHub profile: <https://github.com/JNCressey>

# Development Projects

## Oldschool RuneScape Wiki

### Location name tooltip enhancement to the Fairycode module

[Read More](blogs/osrswiki/modulefairycode.md)

### Recipe steps profit comparison table

[Read More](blogs/osrswiki/recipesteps.md)


## RuneLite

### Plugin for RuneLite: No Hint-Arrow

[Read More](blogs/runelite/nohintarrow.md)


## Minecraft

### A datapack to generate randomised dungeons

[Read More](blogs/minecraft/jigsawdungeon.md)

## Tzar: The Burden of the Crown

### Attempt to document the AI scripting language and configurable game constants 

[Read More](blogs/tzar/redocument.md)

## Barcodes

### Barcode sheet generator 

[Read More](blogs/barcodes/barcodesheetgenerator.md)

## Coding Challenges

### A solver for the Tower of Hanoi puzzle using memorised iteration instead of recursion

[Read More](blogs/codingchallenges/hanoinorecursion.md)

### The sequence of bet amounts when using the Martingale strategy

[Read More](blogs/codingchallenges/martingalegambling.md)

### Parker's Maths Puzzles 'MPMP: The 1 Million Bank Balance puzzle'

[Read More](blogs/codingchallenges/mpmpbank.md)

### My submitted strategy for Carykh's Prisoner Dilemma Tournament

[Read More](blogs/codingchallenges/prisonerdilemma.md)
