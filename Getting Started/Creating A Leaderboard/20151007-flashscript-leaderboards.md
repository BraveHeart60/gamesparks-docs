title: ActionScript Leaderboards
link: https://docs.gamesparks.net/documentation/request-api/leaderboards-request-api/flashscript-leaderboards
author: omar.albadry
description:
post_id: 9197
created: 2015/10/07 13:56:24
created_gmt: 2015/10/07 12:56:24
comment_status: closed
post_name: flashscript-leaderboards
status: publish
post_type: post

# ActionScript Leaderboards

[toc]

## *Introduction*

The previous tutorial taught you how to [create a Leaderboard](/tutorials/creating-a-leaderboard) and Event that submits your Player's score. Now you can incorporate them into your ActionScript project. For the sake of this tutorial we have created a sample game that runs for 10 seconds. In those 10 seconds the Player must collect as many points as possible. If the Player beats the current high score, they will be notified by a message. *Setting up the Event Log Request*

  * Set up a function that logs the Event that submits the Player's score.
*Creating the Message Handler*

  * Create a message handler that listens for the message type NewHighScoreMessage.
  * Create a function that handles the NewHighScoreMessage.
*Testing the Leaderboard*

  * Play your game and beat the high score to receive a message.
[wpdm_file id=36 title="true" ]

## *Setting up the Event Log Request *

You will need a function that calls the Event that submits the Player's score. Make a function that builds the *LogEventRequest* to pass through the score value. The *requestBuilder* has been triggered for when the timer of the game reaches 0. The Player's score will be sent after the game session ends. Call the previously made *Event key* of the Event (for more information see the Portal's Leaderboards tutorial) and set the _SCORE_ attribute.


    	  if (endTime <= now)
    			  {
    				timer.stop();
    				requestBuilder.createLogEventRequest().setEventKey("Leaderboard_Score").setNumberEventAttribute("SCORE", Score).send(ScoreResponse);
    				SpriteWrapper.removeChildren();
    				RestartBtn.enabled = true;
    				logger("Times up");
    			  }


## *Setting up the Message Handlers*

Once you've set your *L**ogEventRequest* to upload the Player's score, you can now set up a *NewHighScoreMessage *handler. *Handlers* are very useful tools which allow you to intercept *messages* that are passed in to your authenticated Player. For this tutorial, we'll be dealing with *NewHighScoreMessage*. We'll place the initialisation of the message handler in the same function which connects the *GS* *module*. To do this use _gs.getMessagerHandler()_ and resume to choose which type of message you wish to intercept, followed by the function which will deal with the message. In our case *'HighScoreMessageListener*' is a variable of type *GS*.


    	gs.getMessageHandler().setNewHighScoreMessageHandler(HighScoreMessageListener);


Create the function which deals with the *message*. The parameters of the function would take a variable of type '*NewHighScoreMessage*'. This function will allow you to simplify the structure of the *message* and access a number of useful data. In this tutorial we retrieve the Leaderboard's name to show the highscore *message* as an alert.


    	private function HighScoreMessageListener(message:NewHighScoreMessage):void
    			{
    				Alert.show("You achieved the highscore in the leaderboard: " + message.getLeaderboardName(), "High Score Alert")
    			}


 

## *Testing the Leaderboard*

Run your game and try to beat the high score. If you do, you will receive a message informing you that you have beaten the high score in that Leaderboard.
![r](img\AS\1.jpg)
