# Bram Salomons

## Introduction

I've been passionate about creating games for as long as I can remember. Back when I was 4 years old, I suddenly thought how cool it'd be if I made the game I was playing at the moment. Not only I would have fun playing that game, but people all over the world could also have fun playing my game if I made games as a job. Now I'm studying CMGT as an engineer to make my dream job a reality, and I'm enjoying every moment of the process.


# Portfolio

## Monster Matches [(Link to Game)](https://battleramgamer.itch.io/monster-matches)




<details>
<summary>Code snippets</summary>
<details>
<summary>Blinking Platform</summary>

Text test
```C#
IEnumerator BlinkPlatformFor(float pSeconds)
{
    // Determining values
    int count = fallCount.GetFallCount(round);
    int[] selectedPlatforms = GetRandomPlatforms(count);
    GameObject[] blinkingPlatforms = CreateBlinkPlatforms(count, selectedPlatforms);
    float blinkStateDuration = pSeconds / blinkStateChangeAmount;

    // Blinking
    for (float i = pSeconds; i > 0.01; i -= blinkStateDuration)
    {
        SwitchBlinkState(blinkingPlatforms);
        yield return new WaitForSeconds(blinkStateDuration);
    }

    // Platform gone
    MakePlatformsDisappear(selectedPlatforms, blinkingPlatforms);
    

    // Time until next platform starts blinking
    yield return new WaitForSeconds(platformDisappearTime);
    MusicManager.Instance?.PlaySound(platformBackSound);

    // Cooldown time between platforms returning and next round
    yield return new WaitForSeconds(restTime);
    OnNewRound?.Invoke();
    StartRound();

}
```

</details>
<details>
<summary>Bibi rotating</summary>

Text 2est

```C#
private void FixedUpdate()
{
    if (!isActive) return;
    if (rotatesClockwise)
    {
        forwardRotationMult = Mathf.Clamp(forwardRotationMult + reverseStrengthPerFrame, -1f, 1f);
    }
    else forwardRotationMult = Mathf.Clamp(forwardRotationMult - reverseStrengthPerFrame, -1f, 1f);
    
    firePivot.transform.localScale = new Vector3(1, 1, fireRetractCurve.Evaluate(Mathf.Abs(forwardRotationMult)));

    DoRotation();
}

void DoRotation()
{
    // Get turn speed
    currentTurnsPerSecond = rotationSpeed.Evaluate(MinigameManager.Instance.GetTimePercent());
    currentDegreesPerFrame = TurnsPerSecToDegPerFrame(currentTurnsPerSecond);

    // Take turning around in account
    actualDegreesTurned = currentDegreesPerFrame * forwardRotationMult;

    // Rotate and write down how much
    transform.Rotate(new Vector3(0, actualDegreesTurned, 0));
    totalDegreesTurned += actualDegreesTurned;
    totalTurns = totalDegreesTurned / 360;

    if (Mathf.Abs(totalDegreesTurned) >= currentTurnFrequency * 360) TurnAround();
}
```

 <p>Bibi rotating and spewing fire in Bibi’s minigame</p>
 <p> <IMG src="Code%20samples/Monster%20Matches/Bibi%20spin.png"  alt="Bibi rotating and spewing fire"/> </p>

</details>
</details>





## Monster Matches [(Link to Game)](https://battleramgamer.itch.io/monster-matches)
* 8 weeks
* Group project (team of 7)
* C#
* Unity

This game was made in Unity in 9 weeks for a school project. For the assignment, we picked [the library](https://www.bibliotheekenschede.nl) as our external client, who participated in [the monster project](https://www.themonsterproject.org). In this scenario, they went to a primary school (International School Twente) and made a class of pupils in the 4th grade come up with and draw their own monster. Our job was to make an interactive product using those monsters, which the library would include in [their exhibition](https://www.bibliotheekenschede.nl/nieuws/monstersindebieb.html). My group decided to make a collection of minigames, with each minigame being themed around one of the monsters we picked. We chose to make the minigames simple and competitive to make sure the pupils would not only enjoy playing the minigame with their own monster, but also the minigames with other monsters. This means simple controls, simple concepts for minigames and (mostly) simple code.

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


## Fading Colors [(Repository)](https://github.com/BattleRamGamer/ProjectCustomer)
* 3 weeks
* Group project (team of 7)
* C#
* Unity

Fading Colors is a serious game that aligns with the goals of the [Alzheimer's Association](https://www.alz.org/), and creates awareness for Alzheimer's. In this game, you play as an artist performing his daily routines while going through a cognitive decline. You perform tasks like making coffee, gathering inspiration and painting.

I mainly worked on programming the core mechanics like grabbing/placing items, interacting with objects and the flow of the game. This was the first game I made in Unity with a multidisciplinary team, which made me realize how easy it is to improve my skills and knowledge when I'm working on a similar task with someone else. In this case, I gained a lot of experience with handy tools in Unity and how to keep the project designer friendly.

<details>

 <summary><h3  style="display:inline-block">Code snippets</h3></summary>
 
 <p>When interacting with an object, this code checks if all requirements are met in order to complete the interaction</p>
 <p> <IMG src="Code%20samples/Fading%20Colors/Requirements%20met.png"  alt="Simple camera movement"/> </p>
 
 <p>Code for an item you can grab. You can only place these items on predetermined locations, and this code handles dialogue, sound and other logic that happens when you grab or place it down</p>
 <p> <IMG src="Code%20samples/Fading%20Colors/Placable%20item.png"  alt="Code for a placable item, checks state of where item is located and handles logic"/> </p>

 <p>Example of organized parameters, allowing the game designer(s) to implement and change logic for interactions</p>
 <p> <IMG src="Code%20samples/Fading%20Colors/Designer%20friendly%20parameters.png"  alt="Organized parameters for interactable"/> </p>
 <p> <IMG src="Code%20samples/Fading%20Colors/Parameters in unity.png"  alt="Organized parameters for interactable, shown in Unity"/> </p>

</details>


