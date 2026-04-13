# Bram Salomons

## Introduction

I've been passionate about creating games for as long as I can remember. Back when I was 4 years old, I suddenly thought how cool it'd be if I made the game I was playing at the moment. Not only I would have fun playing that game, but people all over the world could also have fun playing my game if I made games as a job. Now I'm studying CMGT as an engineer to make my dream job a reality, and I'm enjoying every moment of the process.


# Portfolio

## Monster Matches [(Link to Game)](https://battleramgamer.itch.io/monster-matches)

#### Description
Monster Matches is a party game for up to 4 players. There are 4 minigames, each taking inspiration from a monster made by an elementary school pupil in group 4 (4th grade). This project was showcased in an [exhibition](https://www.bibliotheekenschede.nl/nieuws/monstersindebieb.html) by [the library](https://www.bibliotheekenschede.nl), who took part in [the monster project](https://www.themonsterproject.org).

#### Challenges
This project lasted 9 weeks, which is the longest project I've worked on. I was mainly responsible for making the minigames. Our first playtest was already two weeks after receiving the assignment, and I managed to get three minigames ready for the playtest, including the hub and navigating to and from those minigames. I also made a reusable system for the minigame loop and scores. After the first playtest, I made the last minigame also playtestable, and after that we essentially had 5 weeks of adding nice to have features and polishing what we already had. The biggest features I made here are pause screen UI navigation and the sound system (with volume sliders).

#### What did I learn
I mainly got to experience what it's like to work on a game for 9 weeks with an amazing team of talented people. This project reminded me of why I love making games and showed me the positive effects of being able to playtest and iterate early

<details>
<summary><h3  style="display:inline-block">Code snippets</h3></summary>

<details>
<summary>Blinking Platform for Cloudy</summary>
<div markdown="1">

```csharp
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
</div>
</details>

<details>
<summary>Bibi rotating and turning around</summary>
<div markdown="1">

```csharp
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

</div>
</details>

<details>
<summary>Finite state machine for Mr. Scary Mouse</summary>
<div markdown="1">

```csharp
private void FixedUpdate()
{
    intensity = intensityCurve.Evaluate(MinigameManager.Instance.GetTimePercent());
    switch (currentState)
    {
        case State.moving: Movement(); break;

        case State.preparing: CheckPrepare(); break;

        case State.cooldown: CheckCooldown(); break;

        case State.pregame:
            transform.position = Vector3.Lerp(lastLocation, newLocation, timer/2f);
            break;

        default:
            timer = 0;
            break;
    }


    timer += Time.fixedDeltaTime;
}
```

</div>
</details>

</details>


___


## Silent Protocol [(Trailer)](https://youtu.be/mgys0usTa20) [(Walkthrough)](https://youtu.be/iB_7-jarEfg) 

#### Description
Silent Protocol is a horror game that features a big ear-shaped monster that chases you if it can hear you. While you mainly play on PC, you also need to enter codes on your phone or physically move it to open doors and progress further in the game. 

#### Challenges
The two main things I worked on here are the pathfinding system and sound system. For the pathfinding system, I made waypoints that only knows where the next location is to allow multiple unique implementations of pathfinding. In this case, there's a laser that just moves directly to the next waypoint, and the monster AI makes use of Unity's built-in NavMeshAgent. The interesting part of the sound system gives each sound a range in which the monster can hear you (and will approach you).

#### What did I learn
Reusable assets are amazing. We sadly had to crunch main functionality in the last week to finish the game, which made me realize the importance of finishing an MVP (Minimum Viable Product) as soon as possible to allow fast iterations.

<details>
<summary><h3  style="display:inline-block">Code snippets</h3></summary>

<details>
<summary>Sound distance checking</summary>
<div markdown="1">

```csharp
public void CheckLoudness(string soundID)
{
    float range = 0;
    //Debug.Log("Looking for " + soundID);

    foreach (SoundLoudness sound in soundData)
    {
        //Debug.Log("Comparing with " + sound.sound.name);
        if (sound.sound.name == soundID)
        {
            //Debug.Log("Name found!");
            range = sound.radius;
            break;
        }
    }

    if (range <= 0)
    {
        //Debug.Log("Nothing was found, please check if the name is correct");
        return;
    }

    CheckMonsterDistance(range);
}
```

```csharp
private void CheckMonsterDistance(float soundRange)
{
    if (soundRange > currentVolume)
    {
        currentVolume = soundRange;
    }
    Vector3 playerPos = PlayerMovement.GetPlayer().transform.position;

    float monsterDistance = Vector3.Distance(monster.transform.position, playerPos);

    if (monsterDistance <= soundRange)
    {
        //Debug.Log("Approaching player");
        monster.HearPlayer();
    }
    else
    {
        //Debug.Log("Distance is too big, not approaching player");
    }
}
```

</div>
</details>

<details>
<summary>Path waypoint logic</summary>
<div markdown="1">

```csharp
public Transform GetFirstPoint()
{
    currentPointIndex = 0;
    return pointLocations[0];
}
public Transform GetNextPoint()
{
    currentPointIndex++;
    currentPointIndex %= numberOfPoints;
    return pointLocations[currentPointIndex];
}
public Transform GetRandomPoint()
{
    // Avoiding getting the same location twice
    int nextPoint = Random.Range(0, numberOfPoints - 1);
    if (nextPoint == currentPointIndex) nextPoint++;
    currentPointIndex = nextPoint;
    return pointLocations[currentPointIndex];
}
```

</div>
</details>

<details>
<summary>Reusable Danger component</summary>
<div markdown="1">

```csharp
public class Danger : MonoBehaviour
{
    [SerializeField]
    private string deathMessage;

    [SerializeField]
    private AudioClip deathSound;

    private AudioSource audioSource;

    private void Start()
    {
        audioSource = GetComponent<AudioSource>();
    }

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            DeathManager.GetMainManager().KillPlayer(deathMessage);
            if (audioSource != null && deathSound != null)
            {
                audioSource.PlayOneShot(deathSound);
            }
        }
    }

}
```

</div>
</details>

<details>
<summary>Easy iteration for laser movement</summary>
<div markdown="1">

```csharp
private enum ConsistentSpeedDirection
{
    X,
    Z,
    Foward
}

[SerializeField]
private ConsistentSpeedDirection consistentSpeedDirection;

private void FixedUpdate()
{
    float secretRealSpeed = speed / 100f;
    Vector3 diff = currentDestination.position - transform.position;
    diff.y = 0;

    switch (consistentSpeedDirection)
    {
        case ConsistentSpeedDirection.X: MoveConsistentX(secretRealSpeed, diff);
            break;
        case ConsistentSpeedDirection.Z: MoveConsistentZ(secretRealSpeed, diff);
            break;
        case ConsistentSpeedDirection.Foward: MoveConsistentForward(secretRealSpeed, diff);
            break;
    }        

}
```

</div>
</details>

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


