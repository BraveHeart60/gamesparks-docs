---
nav_sort: 1
---

# Unity Cloud Code

## Introduction

GameSparks offers a lot of useful features out of the box, like Challenges, Leaderboards and Messaging systems. However, our Cloud Code also allows you to create your own custom Events to pass the data to and from the servers. In this tutorial you are going to use two Events to save and load some basic player information. You don’t need anything extra to follow this tutorial, but if you’d like to see our project example you can download it here. [wpdm_file id=25 title="true" ]

## Creating Event

![l](img/UT/1.png)

You can create Events in your GameSparks Portal by going to the *Events* tab and clicking on the *[+]* button on the right of the page. Create an Event that will save some player details. Click on the *[+] *button and follow these steps:

1. *Short Code* - This is a unique code used to define this Event when it is called.
2. *Name* - This is used to identify the Event within the Portal.
3. *Description* - A few details that explain the Event.
4. *Attributes* - These are the values that the Event will take. Effectively the data the Event will take from the client to the server (from Unity to GameSparks). In this example we will save the player’s experience points, position and gold. We will load these later with another method.

## Calling the Event Request

You can call the Events in Unity using the *LogEventRequest* method. This a default method that will take some variable data depending on what you need. In contrast with the other requests you have used in previous tutorials, the *LogEventRequest* needs information about the attributes and keys before you send the request.

### Saving Player Data

Calling the *LogEventRequest* method works as follows:

```
    new GameSparks.Api.Requests.LogEventRequest().SetEventKey("SAVE_PLAYER").SetEventAttribute("XP", 123456).SetEventAttribute("POS", playerPosition.ToString()).SetEventAttribute("GOLD", 100).Send((response) => {
    	if (!response.HasErrors) {
    		Debug.Log("Player Saved To GameSparks...");
    	} else {
    		Debug.Log("Error Saving Player Data...");
    	}
    });
```

![l](img/UT/2.png)

![l](img/UT/3.png)

The *LogEventRequest* will execute the custom Event you have created. You will need to provide the Event short code that was previously defined when creating the Event to the logEventRequest. You will also need the keys of the Event attributes you've set in your Event. In this case they are experience point (XP), position (POS) and gold (GOLD).  If you have the Sample Project open, you can enter these details in the scene and hit the *Save Player* button. You should see GameSparks sending and receiving this request in the console.


### Saving the Data in GameSparks

Now you've sent the logEventRequest from Unity, you will now be able to save the Players details in GameSparks. To do this, you need to set some custom Cloud Code in the GameSparks Portal. You can see how to navigate to your Event on the right. In the Cloud Code editor, you will be able to access the data sent via Unity, you can then add this as the Player data to your collection.

```
    var playerDataList = Spark.runtimeCollection("playerData"); // this will get the collection of player data
    var playerID = Spark.getPlayer().getPlayerId(); // first we get the id of the current player
    var playerExperiance = Spark.getData().XP; // we get the xp input from Unity
    var playerGold = Spark.getData().GOLD; // Get the gold input from Unity
    var playerPos = Spark.getData().POS; // and the position input from Unity
    var currentPlayer = {
    	"playerID": playerID,
    	"playerXP": playerExperiance,
    	"playerGold": playerGold,
    	"playerPos": playerPos
    }; // we construct a new player from the data we are about to input into the player data
    playerDataList.update({
    	"playerID": playerID
    }, //Looks for a doc with the id of the current player
    {
    	"$set": currentPlayer
    }, // Uses the $set mongo modifier to set old player data to the current player data
    true, // Create the document if it does not exist (upsert)
    false // This query will only affect a single object (multi)
    );
```

Make sure to hit the *Save* button in order to save the Cloud Code for your Event.

![l](img/UT/4.png)

## Testing your Cloud Code

![l](img/UT/5.png)

You can now head back to Unity and run your* LogEventRequest* with some XP and gold values. In the next section you are going to get that data back from your GameSparks game, but if you want to check that your player’s data was updated, you can select the* playerData* collection from the *NoSQL Explorer* tab, and click the *Find* button.


## Loading Data

Loading the data will work in a similar fashion. You need to create an Event called LoadPlayer, this Event doesn't require any Event attributes as we will not be passing any data into it. First you will have to create an Event. Then before you head back to Unity, you will need to write some Cloud Code for this Event. All you need to do is grab the entry in your playerData collection that corresponds to the player ID of the current player, and return that player’s data via the script data.

```
var playerData = Spark.runtimeCollection("playerData"); // get the collection data
var currentPlayer = playerData.findOne({
	"playerID": Spark.getPlayer().getPlayerId()
}); // search the collection data for the entry with the same id as the player
Spark.setScriptData("player_Data", currentPlayer); // return the player via script-data
```

![l](img/UT/6.png)  

![l](img/UT/7.png)

## Testing the Load Event

You can test your Events in the *Test-Harness*. You can get to this section by clicking on the *Test Harness* tab on the left hand side of the GameSparks Portal. You will need to authenticate yourself as one of your registered players, then you can select your *LoadPlayer* logEventRequest and run the Event by clicking on the *Send* button. By running the Event you should see your Script Data output in the inspector window as seen in the image.

![l](img/UT/8.png)

![l](img/UT/9.png)

From this set of data you will load the information into a sorted form and output it in Unity. You can call the *LoadPlayer* logEventRequest the same way you did when requesting the *SavePlayer* Event. In this example you will only be interested in the data that comes back from the Portal, specifically the *ScriptData*. There are plenty of ways to extract data from your response, this is just one of the methods I like to use because it allows you to get the data you want using the attribute keys, and it’s very handy when you have multiple sets of data to extract from the data bundle.

```
new GameSparks.Api.Requests.LogEventRequest().SetEventKey("LOAD_PLAYER").Send((response) => {
	if (!response.HasErrors) {
		Debug.Log("Received Player Data From GameSparks...");
		GSData data = response.ScriptData.GetGSData("player_Data");
		print("Player ID: " + data.GetString("playerID"));
		print("Player XP: " + data.GetString("playerXP"));
		print("Player Gold: " + data.GetString("playerGold"));
		print("Player Pos: " + data.GetString("playerPos"));
	} else {
		Debug.Log("Error Loading Player Data...");
	}
});
```

![l](img/UT/10.png)

## Summary

You've had a look at Log Event requests and how they can be used to send and receive data from GameSparks games. You've also learned how to create custom collections for storing information, such as player details. GameSparks also comes with some of its own special kinds of collections such as Leaderboards. In the next tutorial we are going to look at setting up a Leaderboard and implement it in Unity.
