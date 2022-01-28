# Deckforce

Deckforce is a game I made with friends as a project during our first semester at Keimyung University.
For our Game Project course, we were asked to develop a game of our choice. We chose to make a multiplayer PvP turn-by-turn card game.

## How the game works

Each player choose a character, and when all players are ready, the game can be launched. The map has multiple spawn points that can be selected.

There are 3 different characters. Each has different values for health, action, and movement.
You start with 5 random cards, then draw a new one at the start of a new turn.
The winner is the player that stays alive the longer.

Currently, the server cannot run at all times, so an offline mode can be used (it can still be played by multiple people).

## Cards

Cards are divided in 3 categories: Damage (Red), Creation (Green) and Manipulation (Blue).
More powerful cards requires more action points.
Damage cards allow you to kill other entities, by throwing fireball or slime balls, using a sword, or using a bow.
Creation cards are used to summon entites, like Slimes, Stones, or Spikes.
Manipulation cards can heal, create a shield, or draw more cards.

Each card is represented by different elements, like the cost, damage, description, and range.
A card has an area type, which is where the card can be placed (diagonally, in a circle...) and an effect type, which is how the card spreads once activated (on a single tile, in a circle...).  
<br/>
Here is the list of all existing cards in the game:
<br/>
 - Arrow (Damage): Shoots diagonally around the player and deals 1 damage. Requires 1 action point
 - Bomb (Creation): Places a bomb somewhere close to the player. The bomb explodes after a turn, dealing 4 damages. Requires 3 action points.
 - Burn (Damage): Burns a target close to the player. It doesn't deal damages, but apply the burn effect. Requires 2 action points.
 - Draw (Manipulation): Draws 2 cards. Requires 4 action points.
 - Ultimate Draw (Manipulation): Draws 4 cards. Requires 7 action points.
 - FireBall (Damage): Throws a fire ball close to the player, dealing 2 damages in a cross pattern. Requires 3 action points.
 - Heal (Manipulation): Heals the player or an ally for 2 points. Requires 3 action points.
 - Infernus (Damage): Creates a devastating area which deals 2 damages to all entities in its area, while applying the burn effect. Requires 6 action points.
 - Shield (Manipulation): Generates a shield of 3 points around the player or an ally. The shield is reduced before the health when taking damages. Requires 4 action points.
 - Fire Spark (Damage): Shoots a small fire ball, which can go really far from the player, and deal 1 damage. Requires 1 action point.
 - Slime Ball (Damage): Shoots a small slime ball. The slime ball deals 1 damage, and applies the slow effect on its target. Requires 3 action points.
 - Slime Summon (Creation): Summons a slime, a small entity fighting alongside you. It has 3 health points, 4 movement points, and can deal 2 damages if it is close enough to an enemy. Requires 5 action points.
 - Spike Summon (Creation): Creates spikes on a single tile. When an entity walks on the spikes, it deals 2 damages to them. The spikes are then destroyed. Requires 5 action points.
 - Stone Pile Summon (Creation): Creates a small stones pile on a tile. Entities cannot walk throught tile with piles on them, but they can be destroyed (they have 5 health points). Requires 3 action points.
 - Stone Golem Summon (Creation): Summons a powerful stone golem. The golem has 7 health points, 3 movement points, and can deal 5 damages if it is close enough to an enemy. Requires 8 action points, and it needs a stone pile on the tile to be summoned.
 - Sword Hit (Damage): Hits a target next to the player, to deal 3 damages. Requires 2 action points.


Somes cards can apply effects to targets. Currently, there are 2 effects:
 - Burn (deals a small amount of damages after the turn of the affected entity)
 - Slow (reduce the number of movement points of an entity by a small amount)
 

## Personnal contribution

On this project, I worked on the communication between the server and the clients.
I created different packages to be used for the communication. Each package represents an action in the game, and contains informations like the id of the player, a card or character, or the name of a card.

Depending on the action (choose a character, move an entity, activate a card...) a package is sent to the server. The server then send the package to other clients.
On these clients, the package is retrieved, and an action is taken depending on the package and the informations it contains.

</br>
I also worked on the cards system. 

The cards are represented by ScriptableObjects. Every card types inherits from a Card object.
The cards have a system to check if they can be activated (check the range, cost, if a target is in range...) once they are released.
If a card can be activated, its effects will be applied, the particles created by the other who worked on the project will be called, the sounds will be played...
The system is generic enough so that new types of cards can be created easily.

<br/>
One important part of the game I also worked on was the battle system.

During a single turn, every entity plays one time. The order of play is determined by a value called initiative. The higher the initiative, the sooner the entity plays.
Once the turn is over, all entities play again, in the same order as before.
Each entity has 30 secondes to play. After 10 turns, the time to play is reduced. Players can also click the 'End Turn' button instead of waiting the end of the 30 seconds.

On the right of the screen is the initiative display. It allows to see the statistics (health, movement and action points, applied effects) of all entities, and they are sorted by their order of play.

<br/>
The last thing I worked on was the UI element displayed at the end of a game. Display differnet message depending on if won or lost, and displays the name of the winner.
