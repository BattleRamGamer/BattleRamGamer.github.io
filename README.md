# Portfolio Bram Salomons


## Monster Matches [(Link to Game)](https://battleramgamer.itch.io/monster-matches)
* 8 weeks
* Group project (team of 7)
* C#
* Unity

This game was made in Unity in 9 weeks for a school project. For the assignment, we picked [the library](bibliotheekenschede.nl) as our external client, who participated in [the monster project](themonsterproject.org). In this scenario, they went to a primary school (International School Twente) and made a class of pupils in the 4th grade come up with and draw their own monster. Our job was to make an interactive product using those monsters, which the library would include in [their exhibition](https://bibliotheekenschede.op-shop.nl/6928/expositie-monsterproject-2025/02-07-2025). My group decided to make a collection of minigames, with each minigame being themed around one of the monsters we picked. We chose to make the minigames simple and competitive to make sure the pupils would not only enjoy playing the minigame with their own monster, but also the minigames with other monsters. This means simple controls, simple concepts for minigames and (mostly) simple code.

I collaborated with two designers, three artists and one other engineer. I mainly worked on programming the four minigames (including the podium that appears at the end), the sound system and the player's controls and physics. This project was a good way for me to experience what it’s like to work on a game in a team setting for longer than a month. 


<details>

<summary><h3>Code snippets</h3></summary>

Core logic for blinking platforms in Cloudy’s minigame
![alt text][cloudy]

Bibi rotating and spewing fire in Bibi’s minigame
![alt text][bibi]

Mr. Scary Mouse uses a finite state machine for its core logic
![alt text][scaryMouse]

</details>

___


## Silent Protocol [(Trailer)](https://youtu.be/mgys0usTa20) [(Walkthrough)](https://youtu.be/iB_7-jarEfg) 
* 3 weeks
* Group project (team of 6)
* C#
* Unity

3-week long school project where the assignment was to make a (digital) product supported by mobile device features, like a camera or accelerometer. We ended up making a horror game, which you play on pc, connected through a server to a phone application. We sadly didn't publish this game due to the many steps involved in the setup and time constraints. We implemented an accelerometer and gyroscope, but I didn't work on that so that's irrelevant for now. I was mostly responsible for bug testing/QA and programming general gameplay elements like the monster's AI, interacting with objects and sound functionality.
My biggest takeaway from this project was realizing the importance of an MVP (minimum viable product) because it makes fast iterations possible.


<details>

<summary><h3>Code snippets</h3></summary>

When a sound is played, this checks how far away it can be heard
![alt text][loudnessCalc] 

Logic for distance checking
![alt text][loudnessCheck]

 
Reusable for anything with a path: used for monster path and lasers
![alt text][path]
 
Reusable component that kills player upon contact
![alt text][danger]
  
Multiple quick versions of the laser, which follows a set path and kills upon impact. Easy to playtest for fast iterations
![alt text][laser]
![alt text][laserValues]

</details>

___

## C++: Turn-based combat game
* +- 6 weeks
* Individual assignment
* C++ 
* (no pre-made engine)

After getting familiar with C#, I learned to program with C++. The final assignment was to make a small turn-based combat game (similar to Pokémon and Final Fantasy) using C++ and SFML. Starting from scratch, I programmed everything ranging from making something appear on screen to clickable buttons to the combat engine itself by completing weekly assignments.  


<details>

<summary><h3>In-game screenshots</h3></summary>

How the game looks
![alt text][homePage]
![alt text][inGame]

</details>
<details>

<summary><h3>Code snippets</h3></summary>

Generating an opponent with random stats
![alt text][randAttributes]
 
A (rectangular) button that’s clickable

![alt text][button]

</details>

___

## 3D Rendering: Shaders, lighting and texturing basics
* +- 6 weeks
* Individual assignment
* MGE (Micro Game Engine)
* OpenGL

The MGE is a very barebones game engine. It’s basically a small collection of C++ classes of basic features to get us started with OpenGL. Using this, I programmed camera movement and (proper) shaders which react to light using ADS and are compatible with a height map and a splat map.


<details>

<summary><h3>Code snippets</h3></summary>

Simple camera rotation controls

![alt text][https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/3D%20Rendering/Cam%20movement.png]
 
Calculating the influence of light (LIGHTCALC)
![alt text][https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/3D%20Rendering/Cam%20movement.png]

</details>


___

___

![hi][test2]


[test2]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/3D%20Rendering/Cam%20movement.png "hi"


![ALT][test]

    ![2alt](test)

![3alt][bibi]

    ![4alt](bibi)

    ![5alt][.\Code samples/3D Rendering/Cam movement.png]

![6alt](Code%20samples/3D%20Rendering/Cam%20movement.png)

[test]: Code%20samples/3D%20Rendering/Cam%20movement.png

[bibi]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Monster%20Matches/Bibi%20spin.png "Bibi rotating and spewing fire"

[cloudy]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Monster%20Matches/Cloudy%20platforms.png "Platforms blinking, disappearing and reappearing"

[scaryMouse]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Monster%20Matches/Scary%20mouse.png "Finite state machine"

[danger]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Silent%20Protocol/Danger.png "Reusable class for anything that kills the player"

[laserValues]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Silent%20Protocol/Laser%20move%20values.png "Selectable values for what direction the speed counts towards"

[laser]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Silent%20Protocol/Laser%20move.png "Laser code"

[loudnessCalc]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Silent%20Protocol/Loudness%20calc.png "Checking how loud a sound is"

[loudnessCheck]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Silent%20Protocol/Loudness%20check.png "Checking if the monster can hear the sound"

[path]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/Silent%20Protocol/Path.png "Reusable path holder"

[button]:https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/C%2B%2B/Clickable%20button.png "Clickable button"

[homePage]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/C%2B%2B/Home%20page.png "Screenshot of the home page"

[inGame]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/C%2B%2B/Ingame%20screenshot.png "Screenshot of gameplay"

[randAttributes]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/C%2B%2B/Random%20attributes.png "Giving a character random stats"

[camMove]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/3D%20Rendering/Cam%20movement.png "Simple camera movement"

[lightCalc]: https://raw.githubusercontent.com/BattleRamGamer/BattleRamGamer.github.io/main/Code%20samples/3D%20Rendering/Light%20calc.png "Calculating the influence of light in shader"
