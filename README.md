# FT_ReloadingAndAmmo
In this focus topic you will work on creating Data Assets for use in a shooting demo game

## Overview
In the last focus topic you worked on handling the Health side of an FPS, in this you'll be working on the opposite side the Ammo and Damaging system. Notice i'm treating these as seperate game mechanics, as they are independent of each other. This is the same as your assessment, you can use another to help demonstrate your focus mechanic, but foucs on one key gameplay mechanic.

In this we will be adding Data Assets to handle and update different types of ammo, and then use these to update the projectile damage system.

## Where to find the relevant scripts

## Task
- Implement the reloading coding to allow a player to reload their weapon, when the ammunition depletes. 
- Implement the passing the data asset information to the projectile to update the projectile values.
## Hints  

### Reloading - TP_WeaponComponent.cpp
This script has the main functioanality for the reloading system, you will need to complete the Reload function.

I have built you a simple delay system and the Fire Method is what you want to edit. Remember to contianrise the functionality, if it's to do with the weapon have it here or in a subclass if it's starting to get too complicated.

## Changes from base project

### AmmoType and Default Ammo

### TP_WeaponComponent.h
Notice we have all the functionality for the firing in this component, even the action mapping for the firing, this is good OOP design as it keeps all the weapon functionality in one place.
I have added a few lines to the weapon component to control the reloading system.
```
/** How much ammo have we got */
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Ammo", meta = (AllowPrivateAccess = "true"))
int AmmoInClip;
/** How damage can we do */
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Ammo", meta = (AllowPrivateAccess = "true"))
int Damage;
/** Store our ammo type */
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Ammo", meta = (AllowPrivateAccess = "true"))
UAmmoType* AmmoType;
```
Notice, that i have added to add the header file for the AmmoType at the top of the script, **Before the generate.h**.
```
#include "CoreMinimal.h"
#include "Components/SkeletalMeshComponent.h"
#include "AmmoType.h"
#include "TP_WeaponComponent.generated.h"
```
I have also update the blueprint BP_PickUp_Rifle (Content->Blueprints->BP_PickUp_Rifle) to set the Ammo Type Data Asset, to a Default AmmoType. 
![The Rifle Blueprint with the deafult ammo type.](Hints/RifleDefaultAmmo.png)

### TP_WeaponComponent.cpp
I have adjsut the fire method to pass temporaliy store the spawned actored and then set the damage value from the weapon component to the projectile.
```
// Spawn the projectile at the muzzle
AFT_ReloadingAndAmmoProjectile* Projectile = World->SpawnActor<AFT_ReloadingAndAmmoProjectile>(ProjectileClass, SpawnLocation, SpawnRotation, ActorSpawnParams);
if (Projectile)
{
	Projectile->Damage = AmmoType->Damage;
}
```

### FT_ReloadingAndAmmoProjectile.h
We have also created a matching damage value in the projectile to store the damage value passed from the weapon.
```
public:
	int Damage;
```
### Input system and binding

### Data Assets for Ammo Types
Note, the data assets are based on a Struct, which means the Primary Data Asset is a C++ file.

## Challenges
Test your might

## Easy 
- Add a new ammo type, with different damage and max ammo capacity.
- Create a new Data Asset Ammo and add to your game.
- Add in a default ammo type that the player reverts to if they run out of ammo for their current weapon or reload with the specail ammo. Think Left 4 Dead, pistols when you get specail ammo.

## Medium
- Add one new attribute to the ammo type that effects the projectile, e.g. Mass/ impact force, Range, Speed or number of bounces.
- Refine the gameplay to better feedback to the player when reloading, out of ammo, or switching ammo types, e.g. the player has a reload time when they pick up new ammo, the ammo stores material applied the the weapon or rounds.
- Refine the gameplay to add a bit more feel to the game, think recall when shoot,  or pushing the player in a jump shoot.

## Hard
- We are using Data Assets to store different types of ammo. However, updating these individually can be difficult, you can use a Data Table, CSV file in Unreal, but there are also difficulties in using a datatable. Although not a task, try to be aware of the tools for managing the data and assets in your games.
- Refine the gameplay, add in a chambering system so if they reload with bullets in the chamber they have one extra round, keeping the extra round the correct ammunition type.
- Notice i have a made you a mini-shooting gallery, make a target that requires a specific ammo type to destroy it.

# Reference
Content is made by Connah Kendrick (Connah.Kendrick@mmu.ac.uk) using the Unreal Engine FPS Template for the MMU 1st year Game Mechanics Module taught to both Game Development and Game Design Students. 