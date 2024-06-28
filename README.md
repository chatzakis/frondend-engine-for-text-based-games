# Frontend engine for creating text-based games for browser
This is a fun project with the noble cause of creating text-based games on the browser, where user input shapes the story's outcome.
## [Play Demo](https://chatzakis.github.io/frondend-engine-for-text-based-games/) 🎮

## Games created
### [The Haunting Within](https://github.com/chatzakis/the-haunting-within-game/) - [**Play**](https://chatzakis.github.io/the-haunting-within-game/index.html) 
**MATURE AUDIENCE ONLY**

## Game structure
The game is structured using a **directed graph** described using a **JSON file**. To avoid confusion it is crucial to visualize the story.
![example-game-graph](https://github.com/chatzakis/frondend-engine-for-text-based-games/assets/122749336/6150aadf-60e3-465d-a23a-5724604dada4)

Those nodes are described in the file **node.json**. Each node contains text describing the state of the story and options that lead to other nodes - parts of the story. 
The player begins from an initial node - state of the game and progresses through their choices to different final states (winning or losing).

## Nodes
All nodes are described in the **'nodes'** property of the JSON file. Each node has an **id** property which sets it apart from the other nodes. 
The nodes must be in arithmetic order in the JSON file. 
The **text** property includes the content of the node - the state of the story. It can include HTML code for better readability and functionality.
The **narration** property sets an audio narration for the current node. The narration is played when the player clicks on the text. 
The **image** property sets a custom background for the current node. Otherwise the **defaultBackground** will be loaded. 
The **options** property describes all the options available from this node.
At the beginning of the JSON file the **starting** node, the **losing** and **final nodes** must be described as shown below: <br>
```html
"initialNode":0,
"finalNodes":[2,4],
"deathNodes":[2],
```
A checkpoint node can be described for the player to return if needed.
```html
"checkpoint": {"node":1, "time":{ "hours": 12, "minutes": 30 }}
```
Example:<br>
```html
{
    "id": "0",
    "text": "Starting Node text",
    "narration:"", "img":"",
    "options": [
      {"id": "1", "text": "Node 0 - Option 1", "target": "1", "feedback":"This option has feedback", "sound":"", "time":"5"},
      {"id": "2", "text": "Node 0 - Option 2", "target": "3", "feedback":"", "sound":"", "time":"5"}
    ]
 }
```
## Options
Each node has 1 or more options excluding the final ones. Each option has the following: <br>
An **id** property.<br>
A **text** property that describes the action.<br>
A **target** property is the node that the player will be transferred to if they make that choice.<br>
A **feedback** property is a message printed when a player clicks an option<br>
A **sound** property that describes the sound effect played when this option is clicked.<br>
A **time** property that describes the average time that this option takes in-game time.<br>
```html
"options": [
        {"id": "1", "text": "Node 0 - Option 1", "target": "1", "feedback":"This option has feedback", "sound":"", "time":"5"},
        {"id": "2", "text": "Node 0 - Option 2", "target": "3", "feedback":"", "sound":"", "time":"5"}
      ]
```
![example-feedback](https://github.com/chatzakis/frondend-engine-for-text-based-games/assets/122749336/2e95ee90-de8a-47f2-b4a1-c234dfde1544)
## Time
The game counts the in-game time spent for each option of the player. This time is randomized by 50% for each option 
If the clock reaches a certain time a certain event can be triggered sending the player to a timeout node.
```html
"starting time":{ "hours": 12, "minutes": 0 },
"endTime":{ "hours": 21, "minutes": 30 },
"timeoutNode": 2,
```
'timeoutNode' is the node where the player will be transferred if they surpass 'endTime'.

## Inventory
The player can pick up items at certain nodes and use them in later nodes to make jumps to other nodes. Essentially to progress through parts of the story. 
The items picked by the player are displayed at the bottom right of the screen.
The inventory is described in the JSON file as shown below.<br>
```html
  "inventory": [
    {"name":"key", "possession": false, "nodeAcquired": [0], "nodeJumps": [{"use":3, "target": 5}]}
]
```
where the 'possession' becomes True when the player reaches the node 'nodeAcquired' and uses the item at node 'use' to go to node 'target'. 
The name of the item must match its icon and the icon must be saved in a .png format.

## Characters and dialogue
The icons of different characters can be displayed in nodes where the text contains dialogue. The dialogue is described using the classes **speech** and **character_name**.
Example: ```Our hero says: <span class='speech protagonist'>'Hello, pretty lady!'</span> and she answers <span class='speech woman'>'Goodmorning, sir!'</span>```
The list of characters is described in the JSON file in the following manner:<br>
```html
  "characters":[
    {"name": "protagonist", "image": "protagonist.png", "color": "cornflowerBlue" },
    {"name": "woman", "image": "woman.png", "color": "hotPink" }
]
```
  where the story's protagonist must always be described as 'protagonist' and their icon is displayed on the left contrary to the interlocutor's icon which is displayed on the right.
  The color property colors the text of the character.
  ![example-dialogue](https://github.com/chatzakis/frondend-engine-for-text-based-games/assets/122749336/ee9730f2-6815-4c31-9c7f-6eb10d045335)

  ## Other JSON parameters
  ```html
  "soundtrack": "./sound/AdhesiveWombat-Night-Shade.mp3",
  "defaultBackground": "bg.jpg",
  "pauseTime": 1000
```
'soundtrack' is the soundtrack of the game 
'defaultBackground' is the default background of the game nodes located in the 'backgrounds' folder.
'pauseTime' is the time between node transitions. Makes the game more dramatic and allows sound effects to be played properly.

## CSS properties
In the beginning of the **styles.css** file, there is a list of variables to customize the UI of the game (colors, fonts).
Further changes can be done to the **styles.css** file for a more specific UI.

## Other changes
You can change the **name of the game**, the **favicon**, and various messages through the HTML files (index, game). 
You can add the names of all those involved in production in the credits file.

## Running locally
In case you want to develop your game **locally** on your computer use the following commands (for Windows OS) with **Admin rights** to run Chrome to **bypass the CORS policy**.
```html
cd C:\Program Files\Google\Chrome\Application
chrome.exe C:\Users\myUser\path-to-game\index.html --disable-web-security --disable-gpu --user-data-dir=~/chromeTemp
```
### main.py
main.py is an early cmd version of the engine built with Python.

### Soundtrack
You can find the soundtrack used for this demo here: [AdhesiveWombat - Night Shade](https://www.youtube.com/watch?v=mRN_T6JkH-c&ab_channel=FreeMusic)

## Have fun!
Remember to **have fun** and **share** your games with the world! 
  
