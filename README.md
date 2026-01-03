# Portfolio Bram Salomons


## Monster Matches [(Link to Game)](https://battleramgamer.itch.io/monster-matches)
* 8 weeks
* Group project (team of 7)
* C#
* Unity

This game was made in Unity in 9 weeks for a school project. For the assignment, we picked [the library](bibliotheekenschede.nl) as our external client, who participated in [the monster project](themonsterproject.org). In this scenario, they went to a primary school (International School Twente) and made a class of pupils in the 4th grade come up with and draw their own monster. Our job was to make an interactive product using those monsters, which the library would include in [their exhibition](https://bibliotheekenschede.op-shop.nl/6928/expositie-monsterproject-2025/02-07-2025). My group decided to make a collection of minigames, with each minigame being themed around one of the monsters we picked. We chose to make the minigames simple and competitive to make sure the pupils would not only enjoy playing the minigame with their own monster, but also the minigames with other monsters. This means simple controls, simple concepts for minigames and (mostly) simple code.

I collaborated with two designers, three artists and one other engineer. I mainly worked on programming the four minigames (including the podium that appears at the end), the sound system and the player's controls and physics. This project was a good way for me to experience what it’s like to work on a game in a team setting for longer than a month. 


<details>
 <summary><h3  style="display:inline-block">Code snippets</h3></summary>
 
 <p>Core logic for blinking platforms in Cloudy’s minigame</p>
 <p> <IMG src="Code%20samples/Monster%20Matches/Cloudy%20platforms.png"  alt="Platforms blinking, disappearing and reappearing"/> </p>
 
 <p>Bibi rotating and spewing fire in Bibi’s minigame</p>
 <p> <IMG src="Code%20samples/Monster%20Matches/Bibi%20spin.png"  alt="Bibi rotating and spewing fire"/> </p>
 
 <p>Mr. Scary Mouse uses a finite state machine for its core logic</p>
 <p> <IMG src="Code%20samples/Monster%20Matches/Scary%20mouse.png"  alt="Finite state machine"/> </p>

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
 
 <summary><h3  style="display:inline-block">Code snippets</h3></summary>

 <p>When a sound is played, this checks how far away it can be heard </p>
 <p> <IMG src="Code%20samples/Silent%20Protocol/Loudness%20calc.png"  alt="Checking how loud a sound is"/> </p>

 <p>Logic for distance checking</p>
 <p> <IMG src="Code%20samples/Silent%20Protocol/Loudness%20check.png"  alt="Checking if the monster can hear the sound"/> </p>

 <p>Reusable for anything with a path: used for monster path and lasers</p>
 <p> <IMG src="Code%20samples/Silent%20Protocol/Path.png"  alt="Reusable path holder"/> </p>

 <p>Reusable component that kills player upon contact</p>
 <p> <IMG src="Code%20samples/Silent%20Protocol/Danger.png"  alt="Reusable class for anything that kills the player"/> </p>

 <p>Multiple quick versions of the laser, which follows a set path and kills upon impact. Easy to playtest for fast iterations </p>
 <p> <IMG src="Code%20samples/Silent%20Protocol/Laser%20move.png"  alt="Laser code"/> </p>
 <p> <IMG src="Code%20samples/Silent%20Protocol/Laser%20move%20values.png"  alt="Selectable values for what direction the speed counts towards"/> </p>

</details>

___

## C++: Turn-based combat game
* +- 6 weeks
* Individual assignment
* C++ 
* (no pre-made engine)

After getting familiar with C#, I learned to program with C++. The final assignment was to make a small turn-based combat game (similar to Pokémon and Final Fantasy) using C++ and SFML. Starting from scratch, I programmed everything ranging from making something appear on screen to clickable buttons to the combat engine itself by completing weekly assignments.  


<details>
 <summary><h3  style="display:inline-block">In-game screenshots</h3></summary>
 <p>How the game looks</p>
 <p> <IMG src="Code%20samples/C%2B%2B/Home%20page.png"  alt="Screenshot of the home page"/> </p>
 <p> <IMG src="Code%20samples/C%2B%2B/Ingame%20screenshot.png"  alt="Screenshot of gameplay"/> </p>
</details>

<details>
 <summary><h3  style="display:inline-block">Code snippets</h3></summary>

 <p>Generating an opponent with random stats</p>
 <p> <IMG src="Code%20samples/C%2B%2B/Random%20attributes.png"  alt="Giving a character random stats"/> </p>

 <p>A (rectangular) button that’s clickable</p>
 <p> <IMG src="Code%20samples/C%2B%2B/Clickable%20button.png"  alt="Clickable button"/> </p>

</details>

___

## 3D Rendering: Shaders, lighting and texturing basics
* +- 6 weeks
* Individual assignment
* MGE (Micro Game Engine)
* OpenGL

The MGE is a very barebones game engine. It’s basically a small collection of C++ classes of basic features to get us started with OpenGL. Using this, I programmed camera movement and (proper) shaders which react to light using ADS and are compatible with a height map and a splat map.


<details>

 <summary><h3  style="display:inline-block">Code snippets</h3></summary>
 
 <p>Simple camera rotation controls</p>
 <p> <IMG src="Code%20samples/3D%20Rendering/Cam%20movement.png"  alt="Simple camera movement"/> </p>
 
 <p>Calculating the influence of light (LIGHTCALC)</p>
 <p> <IMG src="Code%20samples/3D%20Rendering/Light%20calc.png"  alt="Calculating the influence of light in shader"/> </p>

</details>


