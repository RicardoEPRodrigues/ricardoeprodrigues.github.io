---
layout: post
category: blog
title: Attaching an Actor to Another in UE5 C++ | Creating and Equipping a Melee
  Weapon in Adfectus
date: 2022-05-20T21:56:59.524Z
description: This tutorial focuses on the creation of a weapon (an Actor in UE5)
  that can be equipped by a character.
image: /assets/uploads/highresscreenshot00007.png
tag:
  - gamedev
  - game
  - ue5
  - c++
author: ricardorodrigues
---
This tutorial focuses on creating a weapon that a character can equip in UE5. This is a follow-up to the [Collisions and Damage in UE5 Tutorial](<{{ site.url }}/combat-in-adfectus-collisions-in-ue5/>). In this tutorial, we will focus on how you can equip a weapon to a character.

We'll start by implementing the essential bits in C++, then we move to Blueprints. The behavior in C++ can be defined in a few steps: **(1)** Create the weapon, **(2)** Attach the weapon to the character, and **(3)** Set the character as the wielder of the weapon. The behavior in the Blueprints will only facilitate the creation and equipping of a weapon.

## The Weapon... Equippable

To equip a weapon, the bulk of the work is performed on the character.

For the weapon itself, we just need to keep the reference to its owner and disable collisions with it. Let's look at how we can do it.

```cpp
UCLASS()
class CPPTHIRDPERSON_API AWeapon : public AActor
{
	GENERATED_BODY()
    
    // Weak Pointer to the wielder.
	UPROPERTY()
	TWeakObjectPtr<class AActor> WielderPtr;
    
public:
    
    // Function to set the wielder.
	UFUNCTION(Category = Weapon)
	void SetWielder(class AActor* Actor);
    
    //...
}
```

In the header, we just need to add the reference and a new function. Recall that the weapon is an actor and can be placed in the scene separate from the character.

```cpp


void AWeapon::SetWielder(AActor* Actor)
{
	if (AActor* Wielder = WielderPtr.Get())
	{
		WeaponMesh->MoveIgnoreActors.Remove(Wielder);
	}
	WielderPtr = Actor;
	if (Actor)
	{
		WeaponMesh->MoveIgnoreActors.Add(Actor);
	}
}
```

The character class will call the `SetWielder` function when equipping a weapon. What we want to do here is to define the new wielder and set it to ignore the collisions with that character (also note how we check the previous wielder and re-enable collisions with it). For the weapon that is it.

Let's look at our character.

```cpp
// Socket name where the weapon will be attached to.
#define RIGHT_WEAPON_SOCKET "Right_Weapon_Socket"

UCLASS(config = Game)
class AMyCharacter : public ACharacter, public IInteractor
{
	GENERATED_BODY()
    //...
    
public:
    // Called when this character is being destroyed.
    // If we have a weapon, we want to destroy it.
    BeginDestroy();
    
	UPROPERTY(Category = Weapon, VisibleAnywhere, BlueprintReadOnly, meta = (AllowPrivateAccess = "true"))
	class AWeapon* EquippedWeapon;
    
	/** Equips given weapon on the character. */
	UFUNCTION(BlueprintCallable, Category = Weapon)
	virtual void EquipWeapon(class AWeapon* Weapon);

	/** Drops Equipped Weapon if it exists. If destroy parameter is true, the weapon is destroyed instead of being dropped. */
	UFUNCTION(BlueprintCallable, Category = Weapon)
	virtual void DropWeapon(bool bDestroy = false);
}
```

In the header of our character, we need a pointer to our weapon and some new functions, to add and remove the weapon.

```cpp

#include "Weapon.h"

void AMyCharacter::BeginDestroy()
{
	DropWeapon(true);
    //...
}

void AMyCharacter::EquipWeapon(AWeapon* Weapon)
{
	if (Weapon != nullptr)
	{
		/* Drop Equipped Weapon */
		DropWeapon();
        /* OR */
		/* Destroy Equipped Weapon. */
		DropWeapon(true);
        
        /* Use this weapon and attach it */
		EquippedWeapon = Weapon;
        /* OR */
		/* Create a copy of the weapon and attaching it. */
		FActorSpawnParameters parameters;
		parameters.Template = Weapon;
		EquippedWeapon = GetWorld()->SpawnActor<AWeapon>(Weapon->GetClass(), parameters);
      
        // Set the wielder, ignore collisions, and add it to the correct socket.
        EquippedWeapon->SetWielder(this);
        MoveIgnoreActorAdd(EquippedWeapon);
        EquippedWeapon->AttachToComponent(GetMesh(),
                                          FAttachmentTransformRules::SnapToTargetNotIncludingScale,
                                          TEXT(RIGHT_WEAPON_SOCKET));
	}
	else
	{
		UE_LOG(LogAdfectus, Warning, TEXT("Weapon is null."))
	}
}

void AMyCharacter::DropWeapon(bool bDestroy)
{
	if (EquippedWeapon != nullptr)
	{
        // Remove from the socket, making it seperate from the character.
		EquippedWeapon->DetachFromActor(FDetachmentTransformRules::KeepWorldTransform);
        // Re-enable collisions.
		MoveIgnoreActorRemove(EquippedWeapon);
      
		if (bDestroy)
		{
			EquippedWeapon->Destroy();
		}
      
		EquippedWeapon = nullptr;
	}
}
```

Here we need a bit more info. Let's focus on the `EquipWeapon()` function. We start by dropping or destroying the former weapon if it exists (explained later). (WIP)

*Add a video example. Add BP weapon example. Add Weapon Pickup BP example.*