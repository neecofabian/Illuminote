# Illuminote

A mixed-reality multiplayer game with a spark.

Learn more on [Devpost](https://devpost.com/software/illuminote)

Watch the [demo](https://www.youtube.com/watch?v=vV_ab0vMUgk)

## What is Illuminote?

While Illuminote is a classic two-player top-down shooter game at heart, it shines with the following features: 
- Arrange sticky notes on the screen to design the game map. Some sticky notes have special abilities.
- Point the phone’s camera towards the screen to calibrate the mixed reality map.
- During the game:
   - Blue player uses the `UP`, `LEFT`, `RIGHT` arrow keys and `SPACEBAR` to navigate and shoot bullets.
   - Red player uses `A`, `W`, `D`, and `SHIFT` to navigate and shoot bullets.
   - Ricochet bullets using yellow sticky notes.
   - Teleport yourself and bullets between the pink sticky notes.
   - Hit your opponent until they no longer illuminate to win!
- Sometimes, **Blackout mode** is activated. At this time, the players cannot see each other, making the game more challenging. The same rules above apply but here are some helpful tips:
   - Shoot glowing bullets to see your surroundings. But beware, they also reveal your location.
   - Your physical sticky notes keep the map visible.
   - Pay attention to the interaction of bullets and players with your map. The sounds hint at what your opponent is doing.

*Try different map designs for a different experience!*

## Inspiration
The driving questions that inspired Illuminote's mechanics are:
- What if you can’t see who you’re fighting?
- What if attacking your opponent has a cost? By having glowing bullets, the enemy can spot you in the dark.
- How can we use physical objects to influence in-game objects in impactful ways? 

## How we built it

### Feature Extraction
We use Canny Edge Detection
![Imgur](https://i.imgur.com/0p9bYq0.png)
Next, extract the largest features from the image and decide which object is likely a screen (using `approxPolyDp` we can guess that the screen will be the largest 4-sided shape).
![Imgur](https://imgur.com/jMwfWWo.png) 
We then apply a transformation matrix to the screen contour to warp the image to a regular perspective. 
![Imgur](https://i.imgur.com/uJV3Wjb.png)

### Finding the contours for the sticky notes

Using the warped image, we split the image into HSV channels and threshold pixels of the image. We then apply morphological transformations (erode and dilate) to preprocess. Finally, we extract the contours using `cv2.findContours`.

![Imgur](https://i.imgur.com/QjXF7Bi.png)

![Imgur](https://i.imgur.com/sqYWQYa.png)

![Imgur](https://i.imgur.com/JzrH2eq.png)

![Imgur](https://i.imgur.com/LbLzRZb.png)

![Imgur](https://i.imgur.com/3EcfLCL.png)

## Challenges we ran into

Many... many challenges especially when trying to extract the sticky note contours. 

## Accomplishments we're proud of
- Illuminote accurately detects the position and colour of sticky notes.
- Cohesion of the game’s theme of light with its main mechanic, Blackout mode.
- The cool effects caused by the player and bullets interacting with the map. Sparks, splashes, and flashes in addition to the sounds give the game its character.
We had a **“WOW WE ME MADE THAT!?”** moment when we first saw the teleportation effect.
- We ultimately answered the questions that initially inspired Illuminote.

## What's next for Illuminote?
We’re extremely proud of how Illuminote turned out. With more time, some improvements to implement are:
- A little polishing and small bug fixes.
- Faster calibration time when scanning the map.
- A redesigned main menu.
- When a player is shot, they get smaller and smaller, until dying. Being smaller makes it easier to dodge bullets to get fading players a better chance.
- 3D audio to help locate opponents during Blackout mode.
- More than 2 players.
- And perhaps a new mode where players can manipulate the map mid-game.

