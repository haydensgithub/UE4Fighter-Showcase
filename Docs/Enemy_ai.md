# Enemy AI

## Design Goal

I wanted the enemies to be more than passive actors in the combat, but rather to draw more interesting gameplay out of the player by force.
To this end, the enemies are aggresive and highly mobile, complimenting the player's advanced moveset. 
The two standard enemies straight up fly.

## Core Architecture

Each enemy was split into two classes: the **controller** and the **enemy** class.
The controller was responsible for what the enemy __wanted__ to do, including where it wanted to move, how to get there, and what attacks to use.
The enemy class was responsible for handling __how__ it got things done. If the controller decided it wanted to attack, the function to handle that logic existed within the enemy class.
Similarly, the logic for handling health and death existed entirely within the enemy class, as was the safe disposal of the controller class on object destruction.

## Enemy Types

### Evil Lantern

This was the first enemy I worked on, and it really hid the devil in the details during development.

The lantern could:
- Shoot a damaging projectile at the player
- Unleash a close-range explosion if it felt the player was too close
- Occasionally sustain a large tracking laser beam



### Second Enemy Type

Describe what made it different.

Talk about:
- different spacing
- different attack pattern
- different movement behavior
- how it forced a different player response

### Boss

Describe the boss as an encounter, not just a bigger enemy.

Talk about:
- larger health pool
- multiple attacks
- phase-like behavior, if present
- attack readability
- pacing the fight
- how the boss tests the player’s understanding of the combat system

## Attack Telegraphing and Feedback

This should be one of the stronger sections.

Explain how enemies communicate their actions before or during attacks.

Example topics:
- startup animations
- sound cues
- particles
- attack timing
- hit reactions
- visual clarity

Example:
Because the game is fast and first-person, enemy attacks needed to be readable without stopping the pace of combat. I used animation, sound, and particle effects to make enemy actions easier to understand during chaotic fights.

## State Management

This is the programming-heavy section.

Keep it short, but mention the AI was organized around states like:

```text
idle
chasing
attacking
stunned / reacting
dead