# Player Combat System

## Design Goal

I set into development inspired by some fast-paced shooters I had played recently, particularly an indie game called Ultrakill. I wanted to make a combat system that resided in a similar niche while still having its own identity.

## Core Responsibilities

The player class takes in the user's input, consults some amount of internal state (health, equipped weapon, etc.), and takes some action in accordance with that data. For example, if the player tries to jump while on the ground, they jump; if the player then tries to jump again midair, they consume their double jump. The player class never directly influences the internal state of the enemy classes; it can only ask them to adjust their own state (such as through an attack).

## Movement and Combat Flow

The player's movement options and weapons are nearly completely decoupled from one another; in practice, they essentially are two separate, parallel state machines. The player can be doing some movement action (dashing, wall jumping, ground-pounding), which is mutually exclusive to all others. The player may be using some weapon for some action (attacking, charging the hammer, throwing the sword), which is mutually exclusive to all others.

## Weapons / Moveset

### Sword

The sword served as a mechanical multitool in the combat's design, being able to do basically anything, but nothing particularly well. It could attack for low damage at range, had serviceable but not great movement options, and reliable but weak basic attacks. It also served as the game's health bar, represented by the color of the sword draining as the player took damage.

### Hammer

The hammer was primarily designed around its secondary abilities, which were two opposing orbs. The blue orb could be detonated to pull all nearby actors towards the center of its large radius. The red orb could be detonated to push all nearby actors away. This created a weapon that allowed for a great deal of spatial control for an experienced player, rewarded further by a sweet-spot hitbox at the edge of the hammer's reach. I would be the first to admit it was probably a bit overpowered, though.

The two weapons have many additional interactions and intricacies, but in the interest of brevity, I won't mention them here.

## Game Feel

My guiding principle with the game's feel was to examine every single discrete event and jam as much audio-visual feedback into it as possible. If an enemy touches the ground, it makes a sound and particle effect. If the player heals, it makes a sound. If an enemy starts attacking, it makes a sound, particle effect, and animation.

The result of this mentality was a game where the player is acutely aware of every little thing happening around them at all times, an end state I am very satisfied with.

## What I Learned

In truth, this was my first major independent project in C++, and the player class took much of the brunt of that inexperience. Many aspects of the class were messy, hard-coded, or could have been done easier using other data structures. Through working with this code, however, I have significantly improved as a programmer and am much happier with the code I've put together in later projects.

In putting together the player class, I also learned a great deal about sound design, 3D animation, and principles of user experience.
