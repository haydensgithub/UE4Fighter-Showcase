# Enemy AI

## Design Goal

I wanted the enemies to be more than passive actors in the combat. Their purpose was to force more interesting gameplay out of the player by pressuring movement, spacing, and weapon choice.
To this end, the enemies are aggressive and highly mobile, complementing the player's advanced moveset. 
The two standard enemies make this clear by fighting from the sky.

## Core Architecture

Each enemy was split into two classes: an enemy controller and an enemy actor.
The controller was responsible for what the enemy wanted to do, including where it wanted to move, how to get there, and what attacks to use.
The enemy class was responsible for handling how it got things done. If the controller decided it wanted to attack, the function to handle that logic existed within the enemy class.
Similarly, the logic for handling health and death existed entirely within the enemy class, as was the safe disposal of the controller class on object destruction.

## Enemy Types

### Evil Lantern

This was the first enemy I worked on, and it really hid the devil in the details during development.

The lantern could:
- Shoot a damaging projectile at the player
- Unleash a close-range explosion if it felt the player was too close
- Occasionally fire a large tracking laser beam

Developing the lantern was not without its troubles. While some parts of the enemy were very easy to put together, such as the projectile, movement, and explosion, others weren't so easy.
The laser attack required a visual representation that stretched from the lantern's mouth to either its maximum range or the ground/player, whichever came first. In addition, it needed to spawn a particle effect at the location of its impact.
This didn't come without a considerable amount of difficulty and vector math.
Additionally, the instance that trailed underneath the lantern, while not relevant to gameplay, took a good time to get looking good. It required working with Unreal Engine's physics system to get up-and-running.

In making the lantern, I learned:
- Simple AI design principles
- Proper ownership between controller and enemy classes
- Safe spawning and disposal of projectiles
- Complex vector math (in relation to the laser)
- How to use UE4.25's cloth system

### Flying Eye

A more mechanically complex enemy, but considerably easier to develop than the first. 
While the first enemy was content to attack the player from a distance, this enemy makes its presence known by constantly dashing towards the player in a highly aggressive manner.
The two complement each other well.

This enemy could:
- Dash repeatedly toward the player, dealing damage
- Occasionally shoot a damaging projectile
- Dash upwards and backward to control distance between itself and the player.

The main development challenge was handling multiple particle trails attached to the enemy's wings, which was necessary to visually sell its movement. 
To solve this, I created a pool of particle systems available to the enemy to draw from dynamically, a solution that worked fine.

In making the flying eye, I learned:
- Niagara particle system pooling
- High-speed collision handling

### Boss

The boss was originally designed as a recurring rival character for a larger version of the game. This first encounter would have appeared at the end of the second level and rewarded the player with the hammer weapon. Because of that role, the boss needed to feel more expressive and complex than the standard enemies while still maintaining readability in first-person.

The boss was considerably more complex than either standard enemy, with
- 4 attack strings (each with several branching points)
- Anti-air counterattacks
- A parry system
- A posture system that rewarded aggressive play
- A baitable aerial counterattack

Developing this fight was actually largely a frictionless experience. By this point, I had learned the main fundamental lessons of enemy development from the other two enemies. I did learn a few things, however.

In making the boss, I learned:
- Mutually exclusive behavior states (in the controller)
- Mutually exclusive actions states (in the enemy)
