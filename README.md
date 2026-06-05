# Bram Salomons

## <a href="/CV/CV Bram Salomons Public.pdf" download="CV Bram Salomons">Download CV</a>

## Introduction

I've been passionate about creating games for as long as I can remember. Back when I was 4 years old, I suddenly thought how cool it'd be if I made the game I was playing at the moment. Not only I would have fun playing that game, but people all over the world could also have fun playing my game if I made games as a job. Now I'm studying CMGT as an engineer to make my dream job a reality, and I'm enjoying every moment of the process.


# Portfolio

<IMG src="Images/Monster Matches/Monster Matches Icon.png"  alt="Monster Matches Icon"/>

## Monster Matches [(Link to Game)](https://battleramgamer.itch.io/monster-matches) [(Walkthrough)](https://youtu.be/m95To8_tVCA)

{% include youtube.html id="m95To8_tVCA" %}

#### Description
Monster Matches is a party game for up to 4 players. There are 4 minigames, each taking inspiration from a monster made by an elementary school pupil in group 4 (4th grade). This project was showcased in an [exhibition](https://www.bibliotheekenschede.nl/nieuws/monstersindebieb.html) by [the library](https://www.bibliotheekenschede.nl), who took part in [the monster project](https://www.themonsterproject.org).

#### Challenges
This project lasted 9 weeks, which is the longest project I've worked on. I was mainly responsible for making the minigames. Our first playtest was already two weeks after receiving the assignment, and I managed to get three minigames ready for the playtest, including the hub and navigating to and from those minigames. I also made a reusable system for the minigame loop and scores. After the first playtest, I made the last minigame also playtestable, and after that we essentially had 5 weeks of adding nice to have features and polishing what we already had. The biggest features I made here are pause screen UI navigation and the sound system (with volume sliders).

#### What did I learn
I mainly got to experience what it's like to work on a game for 9 weeks with an amazing team of talented people. This project reminded me of why I love making games and showed me the positive effects of being able to playtest and iterate early

<details>
 <summary><h3 style="display:inline-block">Gallery</h3></summary>
 <p>Early version</p>
	<p> <img width="1013" height="572" alt="BibiProgress" src="https://github.com/user-attachments/assets/f5b46bc8-ea39-4945-8405-83388fde1a7f" /></p>
	<p> <img width="1017" height="578" alt="PotatoPrototype" src="https://github.com/user-attachments/assets/27ed7511-0631-41fb-be7a-894fb0b1a204" /></p>
	<p> <img width="1021" height="572" alt="CloudyPlatformBlink" src="https://github.com/user-attachments/assets/25f58e96-ffbc-4e6c-862b-9880becfeb4a" /></p>

 <p>Finished version</p>
 <p> <IMG src="Images/Monster Matches/CurrentPotato.png"  alt="Current gameplay screenshot featuring Potato"/> </p>
 <p> <IMG src="Images/Monster Matches/StartScreen.png"  alt="Starting screen"/> 

</details>

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

<IMG src="Images/Silent Protocol/computer version of logo.png"  alt="Silent Protocol logo"/>

## Silent Protocol [(Trailer)](https://youtu.be/mgys0usTa20) [(Walkthrough)](https://youtu.be/iB_7-jarEfg) 

{% include youtube.html id="iB_7-jarEfg" %}

#### Description
Silent Protocol is a horror game that features a big ear-shaped monster that chases you if it can hear you. While you mainly play on PC, you also need to enter codes on your phone or physically move it to open doors and progress further in the game. 

#### Challenges
The two main things I worked on here are the pathfinding system and sound system. For the pathfinding system, I made waypoints that only knows where the next location is to allow multiple unique implementations of pathfinding. In this case, there's a laser that just moves directly to the next waypoint, and the monster AI makes use of Unity's built-in NavMeshAgent. The interesting part of the sound system gives each sound a range in which the monster can hear you (and will approach you).

#### What did I learn
Reusable assets are amazing. We sadly had to crunch main functionality in the last week to finish the game, which made me realize the importance of finishing an MVP (Minimum Viable Product) as soon as possible to allow fast iterations.

<details>
 <summary><h3 style="display:inline-block">Gallery</h3></summary>
 <p>Early footage</p>
	<p> <img width="1018" height="489" alt="LaserVariations" src="https://github.com/user-attachments/assets/90a31024-f31d-499f-8b1e-1569c04a70f6" /></p>

 <p> <img width="973" height="329" alt="Dying" src="https://github.com/user-attachments/assets/323e0337-9910-454e-892e-681c5abb9915" /></p>

 <p>Gameplay</p>
 <p> <IMG src="Images/Silent%20Protocol/Gameplay.png"  alt="Gameplay screenshot"/> </p>
 <p>Reusable components</p>
 <p> <IMG src="Images/Silent Protocol/Reusable inspector.png"  alt="Unity inspector showing reusable components"/> </p>
</details>

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

<IMG src="Images/Fading Colors/painting3.png"  alt="Fading Colors painting"/>

## Fading Colors [(Repository)](https://github.com/BattleRamGamer/ProjectCustomer) [(Walkthrough)](https://youtu.be/Lh-41ElzN2I) 

{% include youtube.html id="Lh-41ElzN2I" %}

#### Description
Fading Colors is a serious game aligned with the goals of the [Alzheimer's Association](https://www.alz.org/) about the cognitive decline that comes with Alzheimer's. Your goal is to keep performing your daily routine as a retired painter, which keeps getting harder and more confusing to do as the cognitive decline worsens. Later you also play as a caregiver to simulate how you can help.

#### Challenges
This was the first game I made in Unity with a multidisciplinary team, so I had to get used to the whole Unity environment. My main task was everything related to interacting and item functionality. I followed a tutorial for a dialogue system, and I made the logic for requiring items to be placed on specific places.

#### What did I learn
I noticed how easy it is to improve my skills and knowledge when I'm working on a similar task with someone else, especially if they're more experienced that me. In this project, I gained a lot of experience with handy tools in Unity and how to keep the project designer friendly.


<details>
 <summary><h3 style="display:inline-block">Gallery</h3></summary>

 <p>Early footage</p>
 <p> <img width="985" height="454" alt="ItemPickupPlace" src="https://github.com/user-attachments/assets/5551e954-2ada-49b9-96d3-ad32cc9b2f61" /></p>

 <p>Gameplay</p>
 <p> <IMG src="https://github.com/user-attachments/assets/89a72c6a-284c-4660-a39a-6b38ed1523a3"  alt="Gameplay GIF"/> </p>
 <p>Comparison between early and late</p>
 <p> <IMG src="Images/Fading Colors/Worsening.png"  alt="Comparison between early game and late game"/> </p>

</details>

<details>
<summary><h3 style="display:inline-block">Code snippets</h3></summary>

<details>
<summary>Interaction requirement check</summary>
<div markdown="1">

```csharp
private bool RequirementsAreMet(string heldObjID, GameObject heldObj)
{
    if (isInteractedWith) return false;
    if (!InteractionRequirementIsMet()) return false;
    if (!IDLinkRequirementIsMet()) return false;

    // Checking held object requirements
    if (!string.IsNullOrEmpty(requiredHeldObjectID))
    {
        if (requiredHeldObjectID != heldObjID)
        {
            DialogueSystem.GetMainDialogueSystem().HandleText(missingHeldObjDialogue, dialogueTimer);
            return false;
        }
        if (destroyHeldObj) Destroy(heldObj);
    }

    return true;
}
```
</div>
</details>

<details>
<summary>Grab item logic (dialogue, sound, etc.)</summary>
<div markdown="1">

```csharp
public GameObject placedOnPlacable
{
    get
    {
        return PlacedOnPlacable;
    }
    set
    {
        if (value != null && value.TryGetComponent(out PlacerScript script))
        {
            PlaySound(placeSFX);
            if (script.placerLinkIDs.Length > 0)
            {
                for (int i = 0; i < script.placerLinkIDs.Length; i++)
                {
                    if (script.placerLinkIDs[i] == objectID) isPlacedRight = true;
                }
            }
        }
        else
        {
            int nr = UnityEngine.Random.Range(0, grabSFX.Length);
            AudioClip sound = grabSFX[nr];
            Debug.Log("Playing grab sound " + nr);
            PlaySound(sound);
            isPlacedRight = false;
            if (!dialogueHasPlayed && grabDialogue != "")
            {
                DialogueSystem.GetMainDialogueSystem().HandleText(grabDialogue, dialogueTime);
                dialogueHasPlayed = true;
            }
        }
        PlacedOnPlacable = value;
    }
}
```

</div>
</details>

<details>
<summary>Designer friendly organized parameters</summary>
<div markdown="1">

```csharp
public class Interactable : MonoBehaviour
{
    public string interactableID = ""; // String identifier for tracking

    [Header("Requirements")]
    public string[] requiredIDLinks; // String array for required object links
    public string[] requiredInteractions; // String array for required interactions
    public string requiredHeldObjectID = ""; // String for required held object
    public bool destroyHeldObj;

    [Header("Dialogue")]
    public float dialogueTimer = 2f;
    public string interactionDialogue = "";
    public string[] missingObjectDialogues;
    public string[] missingInteractionDialogues;
    public string missingHeldObjDialogue;

    [Header("Object Spawning")]
    public GameObject interactionSpawnsPrefab = null;
    public Transform interactionSpawnPos = null;
    public string giveObjectID = ""; // String for object ID
    public float spawnTime = 2;
    public bool selfDestruct;

    [Header("Misc")]
    public AudioClip interactionSFX = null;
    AudioSource audioPlayer;

    // Functions not included
}
```

</div>
<p> <IMG src="Code%20samples/Fading%20Colors/Parameters in unity.png"  alt="Organized parameters for interactable, shown in Unity"/> </p>
</details>

</details>


___

<IMG src="Images/C++/blue.png"  alt="Turn-based combat game player"/>

## Turn-based combat in C++ [(Walkthrough)](https://youtu.be/dvS_ZTx8yX4) 

{% include youtube.html id="dvS_ZTx8yX4" %}

#### Description
A small endless turn-based combat game that progressively gets harder at higher scores

#### Challenges
After getting familiar with C#, it was time to learn C++. I started with creating a simple text-based combat system and added new features every week like rendering text and images with SFML or a button you can click, and eventually made the full game.

#### What did I learn
I learned how to use C++ and handle memory efficiently by using pointers and references


<details>
 <summary><h3 style="display:inline-block">Gallery</h3></summary>
 <p>How the game looks</p>
 <p> <IMG src="Images/C%2B%2B/Home%20page.png"  alt="Screenshot of the home page"/> </p>
 <p> <IMG src="Images/C%2B%2B/Ingame%20screenshot.png"  alt="Screenshot of gameplay"/> </p>
</details>

<details>
<summary><h3  style="display:inline-block">Code snippets</h3></summary>

<details>
<summary>Generating a new character</summary>
<div markdown="1">

```cpp
void Character::GenerateNewCharacter(const int score, const int baseDistribution) {

    int baseChance = 20;
    int extraChance = 5 * (score / 3);
    int extraPoint = rand() % 100 < (baseChance + extraChance) ? 1 : 0;
    int totalDistribution = baseDistribution + extraPoint - 2;

    strength = 1;
    wits = 1;
    agility = 0;

    for (int i = 0; i < totalDistribution; i++) {
        switch (rand() % 3) {
        case 0:
            strength++;
            break;
        case 1:
            wits++;
            break;
        default:
            agility++;
            break;
        }
    }

    health = strength * 3;
    sanity = wits * 2;

}
```
</div>
</details>

<details>
<summary>Button</summary>
<div markdown="1">

```cpp
bool Button::IsMouseOnButton(const sf::Vector2i mousePos) const {
    
    if (mousePos.x >= GetPos().x + 0 &&
        mousePos.y >= GetPos().y + 0 &&
        mousePos.x <= GetPos().x + shape.getSize().x &&
        mousePos.y <= GetPos().y + shape.getSize().y) 
    {
        return true;
    }

    return false;
}

void Button::update() {

    shape.setPosition(GetPos());
	setText(textStr);
    text.move(shape.getSize().x / 2, shape.getSize().y / 2);

    sf::Vector2i mousePos;

	// Detect if button is being pressed
    if (sf::Mouse::isButtonPressed(sf::Mouse::Left))
    {
        if (!pressed) {
            mousePos = sf::Mouse::getPosition(window);
            pressed = true;

            if (IsMouseOnButton(mousePos)) onClick();
        }
    }
    else {
        pressed = false;
    }

}
```

</div>
</details>

<details>
<summary>Check if new opponent needs to be spawned</summary>
<div markdown="1">

```cpp
bool GameManager::IsOpponentAlive() {

	if (opponent->getHealth() > 0 && opponent->getSanity() > 0) return true;

	AddText("Opponent died!");
	AddText("");
	score++;

	NextOpponent();

	return false;
}

void GameManager::NextOpponent() {

	opponent->GenerateNewCharacter(score, 6);
	enemySprite->setTexture(*getRandomTexture());

	AddText("New opponent joined the battle");
	AddText("");

}
```

</div>
</details>

</details>






___

## C++ Collision Detection (Work In Progress) [(Repository)](https://github.com/BattleRamGamer/AdvRendering) [(Showcase)](https://youtu.be/NTtKeQkA39c)

{% include youtube.html id="NTtKeQkA39c" %}

#### Description
This is made for a self-made collision detection system using AABBs (Axis Aligned Bounding Boxes) and Spheres. I used MGE (Micro Game Engine, a game engine provided by my teachers which only has things like rendering and managing update calls) as a base, and I'm planning to test performance for different implementations to see what works best.

#### Challenges
My focus is not detecting collisions for advanced shapes, but mainly creating a system that efficiently calls the collision checks. I've already made a working version that detects collisions and writes the data (how long each frame takes, how many checks are performed, collisions happening, etc.) to a file, and soon I'll finish up implementing spatial partitioning by following [a guide](https://gameprogrammingpatterns.com/spatial-partition.html), after which I'll create a variation I came up with myself. I'll measure peformance for all variations, put them in a graph and compare them to see which variations are better.

#### What did I learn
By the end, I'll have made my own collision detection system from scratch, made multiple variations of implementations (including a unique method I came up with myself) and researched which have better performance.


<details>
 <summary><h3 style="display:inline-block">Gallery</h3></summary>
 <p>This is how the guide handles the spatial partitioning. It makes a grid of cells, puts each collider in a cell that correlates with its position and makes each collider check collision with the cell it's in and four surrounding cells</p>
 <p> <IMG src="Images/CollisionDetection/Guide spatial partitioning.png"  alt="The way the guide handles spatial partitioning"/> </p>
 <p>Below is a sketch of my variation on the spatial partitioning. The theory here is that, if all colliders are at most 1/3 the size of a cell, you can overlay three grids, each with an offset of 1/3 the size of a cell, and all colliders will always completely fit in at least one cell. Now a collider only needs to check collisions with its own cell and the four cells in the other grids that cell overlaps with</p>
 <p> <IMG src="Images/CollisionDetection/Own spatial partitioning.png"  alt="My variation of spatial partitioning"/> </p>
</details>

<details>
<summary><h3  style="display:inline-block">Code snippets</h3></summary>

<details>
<summary>Collider class</summary>
<div markdown="1">

```c++
#ifndef COLLIDER_HPP
#define COLLIDER_HPP

#include "mge/core/GameObject.hpp"
#include "mge/config.hpp"

class AABB;
class Sphere;

class Collider : public GameObject {

	public:
		Collider(float pX, float pY, float pRadius, bool pAabb);
		~Collider();

		virtual bool checkCollision(Collider* pCollider) const;


		bool checkCircleCircleCollision(Collider* pCollider) const;
		bool checkAABBCircleCollision(Collider* pCollider) const;
		bool checkCircleAABBCollision(Collider* pCollider) const;
		bool checkAABBAABBCollision(Collider* pCollider) const;

		virtual bool checkCollision(AABB* pCollider) const;
		virtual bool checkCollision(Sphere* pCollider) const;

		float getRadius() const;
		bool getIsAABB() const;
	protected:
		float radius;
		bool isAABB;


};

#endif // COLLIDER_HPP

```

</div>
</details>

<details>
<summary>Collider subclass to test double dispatch</summary>
<div markdown="1">

```c++
#include "AABB.hpp"


AABB::AABB(float pX, float pY, float pRadius) : Collider(pX, pY, pRadius, true){

}
AABB::~AABB() {
	//dtor
}


bool AABB::checkCollision(Collider* pCollider) const {
	if (!config::USE_DOUBLEDISPATCH) {
		return Collider::checkCollision(pCollider);
	}
	return pCollider->checkCollision((AABB*)this);
}


bool AABB::checkCollision(AABB* pCollider) const {

	return checkAABBAABBCollision((Collider*)pCollider);
}

bool AABB::checkCollision(Sphere* pCollider) const {

	return checkAABBCircleCollision((Collider*)pCollider);

}
```

</div>
</details>

<details>
<summary>CollisionManager calling for collision checks</summary>
<div markdown="1">

```c++
#include "CollisionManager.hpp"
#include "mge/config.hpp"


CollisionManager::CollisionManager() : testAmount(0) {

}


CollisionManager::~CollisionManager() {
	delete(redMaterial);
	delete(greenMaterial);
}

void CollisionManager::addCollider(Collider* pCollider) {
	_colliders.push_back(pCollider);
}

void CollisionManager::removeCollider(Collider* pCollider) {
	_colliders.push_back(pCollider);
	_colliders.erase(std::remove(_colliders.begin(), _colliders.end(), pCollider));
}

int CollisionManager::checkCollisions() {
	int total = 0;
	testAmount = 0;

	if (!config::USE_IGNOREHISTORY) {
		total = checkCollisionsUnoptimized();
	}
	else {
		total = checkCollisionsIgnoreHistory();
	}


	return total;
}

int CollisionManager::checkCollisionsUnoptimized() {
	int total = 0;
	for (int i = 0; i < _colliders.size(); i++) {
		// If no collisions, this will stay until the end
		_colliders[i]->setMaterial(redMaterial);
		for (int j = 0; j < _colliders.size(); j++) {
			if (i != j) {
				testAmount++;
				if (_colliders[i]->checkCollision(_colliders[j])) {
					total++;
					//_colliders[i]->setMaterial(mats[_colliders[i].colTotal]); or 
					// If there's a collision, set to appropiate colour
					_colliders[i]->setMaterial(greenMaterial);
				}
			}
		}
	}

	return total;
}

int CollisionManager::checkCollisionsIgnoreHistory() {
	for (int i = 0; i < _colliders.size(); i++) {
		// If no collisions, this will stay until the end
		_colliders[i]->setMaterial(redMaterial);
	}

	int total = 0;

	for (int i = 0; i < _colliders.size(); i++) {
		for (int j = i + 1; j < _colliders.size(); j++) {
			if (i != j) {
				testAmount++;
				if (_colliders[i]->checkCollision(_colliders[j])) {
					total++;
					// If there's a collision, set to appropiate colour
					_colliders[i]->setMaterial(greenMaterial);
					_colliders[j]->setMaterial(greenMaterial);
				}
			}
		}
	}

	return total;
}

int CollisionManager::getTestAmount() {
	return testAmount;
}
```

</div>
</details>

</details>


