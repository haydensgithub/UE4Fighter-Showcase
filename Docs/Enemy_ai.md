## Design Goal

I wanted the enemies to be more than passive actors in the combat, but rather to draw more interesting gameplay out of the player by force.
To this end, the enemies are aggresive and highly mobile, complimenting the player's advanced moveset. 
The two standard enemies make this clear by fighting from the sky.

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

Devloping the lantern was not without it's troubles. While some parts of the enemy were very easy to put together, such as the projectile, movement, and explosion, others weren't so easy.
The laser attack required a visual representation that stretched from the lantern's mouth, to either it's maximum range or the ground/player, whichever came first. In addition, it needed to spawn a particle effect at the location of it's impact.
This didn't come without a considerable amount of diffiuclty and vector math.
Additionally, the intestine which trailed underneath the lantern, while not relevant to gameplay, took a good time to get looking good. It required working with Unreal Engine's physics system to get up-and-running.

In making the lantern, I learned:
- Simple AI design principles
- Proper ownership between controller and enemy classes
- Safe spawning and disposal of projectiles
- Complex vector math (in relation to the laser)
- How to use UE4.25's cloth system


### Flying Eye

A more mechanically complex enemy, but considerably easier to develop than the first. 
While the first enemy was content to attack the player from a distance, this enemy makes it's presense known by constantly dashing towards the player in a highly aggresive manner.
The two compliment each other pretty well.

This enemy could:
- Successively towards the player, dealing damage
- Occasionally shoot a damaging projectile
- Dash upwards and back to control distance between itself and the player

The only hangups during development were handling multiple particle trails attached to the enemy's wings, nessecary to visually sell its movement. 
To solve this, I created a pool of particle systems available to the enemy to draw from dynamically; a solution that worked fine.

In making the flying eye, I learned:
- Niagara particle system pooling
- High-speed collision handling


### Boss

When I was developing this project, I had originally intended for it to eventually become a fully fledged game (this was before I really understood proper scoping). 
Within that context, this boss was developed with the intention of being a recurring character, surviving the intial conflict and returning several times throughout the game, the player aquiring a new weapon from them each time.
This first fight would've taken place at the end of the second level and rewarded the player with the hammer weapon; up until then they would have had just the sword.

The boss was considerably more complex than either standard enemy, with:
- 4 attack strings (each with several branching points)
- Anti-air counterattacks
- A parry system
- A posture system which rewarded aggresive play
- And a baitable "get off me" attack in the air

Devloping this fight was actually largely a frictionless experience. By this point, I had learned the main funamental lessions of enemy devlopment from the other two enemies. I did learn a few things, however.

What I learned:
- Mutually exclusive behavior states (in the controller)
- Mutually exclusive actions tates (in the enemy)
