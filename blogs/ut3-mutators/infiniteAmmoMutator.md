# Unreal Tournament 3 Mutator: Infinite Ammo

My repo: [https://github.com/JNCressey/UnrealTournament3-InfiniteAmmoMutator](https://github.com/JNCressey/UnrealTournament3-InfiniteAmmoMutator)

## Intro

The computer game "Unreal Tournament 3" has a system for small modifications to be selected when you start a game. It calls these small mods “mutators”. I made a mutator that gives the weapons infinite ammo.

I was looking through the available community-made mutators on unreal archive for ones that interested me to add to my game, when I wanted one that would give the weapons infinite ammo. There wasn’t one so I decided to make it.

## How it works

I achieved giving weapons infinite ammo by writing an actor class that my mutator spawns an instance of for every weapon that is spawned. After spawning, it is also given a reference to the weapon that it will manage.

The infinite ammo provider hooks into the event that triggers each game tick, and refills the ammo count to its maximum.

## The bug with deployable items

Deployable items are special weapons that are meant to be single-use, and don’t let you switch to a different weapon until you’ve used it. When these were given infinite ammo, it would result in the player being stuck holding the item bring unable to switch to a different weapon. I prevented this situation by excluding deployables from being given an infinite ammo provider.

## Cosmetic design decisions

There are some decisions I made for the implementation that just affect how the heads-up-display looks.
-	I also set the maximum ammo count to 999 so that it is clearly visually different from normal gameplay of having full ammo. This will be a reminder to the player that the ammo is infinite.
-	Normally, when you pick up ammo, the HUD indicates this by flashing the ammo count in larger text. Before I implemented the ammo restoration by hooking into the tick event, I had it run on a repeating timer. However this caused the HUD to flash as though ammo had been picked up. After I changed it to run on the tick event, it no longer flashed.
-	The impact hammer is a weapon that doesn’t use ammo. I excluded it from being given an infinite ammo provider, so that the 999 ammo count doesn’t show up when using that weapon.

## Different options for the players

The Redeemer is a powerful weapon that is supposed to only have 1 ammo, so I excluded it from being given infinite ammo in the main version of the mutator. Unlike deployables, the Redeemer behaved OK when given infinite ammo, so I included an additional mutator in the same package that gives the Redeemer infinite ammo if players wish to have fun with that. 

The Enforcer is a basic weak weapon that typically doesn’t have any ammo pickups. I included an additional mutator that only gives the Enforcer infinite ammo. This provides an experience closer to a normal game where most weapons can run out of ammo, but allows the relatively-weak Enforcer to be more of a safety net by not running out of ammo.

The Longbow AVRiL is a niche weapon meant for combat against vehicles. I included a mutator that only gives the Longbow AVRiL infinite ammo. This would slightly affect the balance of players not in vehicles against players in vehicles without affecting other weapons.




