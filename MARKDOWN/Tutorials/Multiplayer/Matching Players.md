---
nav_sort: 1
src: /Tutorials/Multiplayer/Matching Players.md
---

# How to Match Players

In this tutorial, we'll create a Match configuration with customised Thresholds in the GameSparks Portal and use this configuration to perform a Match in the Test Harness that will match Players in the game. As a brief example of these features, you may want to match Players based on their similar skill level in your game, so that Players can play against someone of equal ability to make it more enjoyable for all.

We'll also see how we can enable:
* Drop In/Drop Out and have matching players added to or removed from the Match after the Match is first made.
* Manual Matching, allowing you to use a custom mechanism for completing a Match from the list of matching players the portal returns for the matching criteria.

## Creating a Match

*1.* To create a Match, navigate to the Portal's *Configurator *and go to the *Multiplayer* section.

*2.* Under *Multiplayer*, click the ![](/img/fa/plus.png) icon for *Matches*:

![](img/HowToMatchPlayers/1.png)

  The *Create Match* form appears:

![](img/HowToMatchPlayers/4.png)

The *Create Match* form contains the following fields:

* *Short Code* \- Enter an identifier for the Match.
* *Name* \- Enter a name for the Match.
* *Description* \- Enter a description of the Match.
* *Min. Players* \- The minimum number of Players for the Match.
* *Max. Players* \- The maximum number of Players for the Match.
* *RealTime* \- Select for a Real-Time Match:
  * *Realtime Script* \- Select a script which will be run on the Real-Time server for the Real-Time Match.
* *Drop In/Drop Out* \- Select for a Drop In/Drop Out Match.
  * *Player disconnect delay in seconds* \- The number of seconds after a Match is found before a player in the Match who disconnects is removed from the Match. If you don't enter a value or enter zero, the player is removed instantly on disconnection.
  * *Expire in seconds* \- The number of seconds after a Match is made that players can drop in or drop out. If you don't enter a value or enter zero, the drop in/drop out period for the Match doesn't expire.
* *Manually match players* \- For custom completion of the matching process. Select this if you do not want the Match to complete automatically when all matching criteria have been met, but want to use your own custom mechanism to complete the Match. The platform will find players for you, but you control the choice of which players are put in the Match.


*3.* In the *Create Match* form, specify the *Short Code*, *Name* and *Description* of your Match and select the ![](/img/fa/plus.png) icon to create the Thresholds you want to use in the Match.


![](img/HowToMatchPlayers/5.png)  

In this example:
* We've added 3 Thresholds to determine player matching: *Absolute*, *Relative*, and *Percent*. (See below: *Working with Thresholds* for how to use these different types of Threshold in a Match.)
* We've specified a minimum of 2 and maximum of 4 players for the Match, which means this will be a *multiplayer Match*:
  * Multiplayer matching is based on synchronous messages that match players based on similar skill attributes, continuously adding players to the Match and updating those already in the Match until the specified maximum number of Players has been reached, similar to the way a Challenge works.
* We haven't selected *Accept Min. Players* for any of the Thresholds. This means that a Match will be found, only when 4 players meet the matching criteria that the Thresholds define.

<q>**Note:** You cannot set the minimum number players for a Match to be fewer that 2. If you set the maximum number of players also at 2, then this is a Head-to-Head Match.</q>

In this example, we haven't:
* Selected for a Real-Time Match and no Realtime script will be executed on the Real-Time server when a Real-Time session starts. You can learn more about Real-Time services [here](/Tutorials/Real-Time Services/README.md).
* Selected for a Drop In/Drop Out Match. (See below: *Using Drop In/Drop Out* for more on how to use this feature for a Match.)
* Selected to Manually match players. (See below: *Manual Matching* for more on how to use this feature for a Match.)
 

*4.* Click to save the Match. The *Create Match* form closes and your Match is added to the *Matches* list under *Multiplayer*:

![](img/HowToMatchPlayers/6.png)

## Working with Thresholds

You can use the Thresholds that you add to a Match configuration to define the criteria that determine player matching. For each Threshold you can define:
* **Threshold Type.** You can choose from three types of Threshold and impose a different degree of precision to the matching process using these types.
* **Threshold Period.** Set a period to control how long you want the matching process to continue trying to find a Match using a Threshold.
* **Accept Minimum Players.** Match the players currently found in the Threshold period that meet the matching criteria, as soon as the number of players found and matched is equal to the value in the *Min. Players* field.

<q>**Example.** Here, we'll use the Thresholds defined for our example Match configuration to explain how you can use Threshold Types and Periods, and how to use Accept Minimum Players for a Threshold.</q>

![](img/HowToMatchPlayers/7.png)  

### Threshold Types

A Match is built upon the different types of range criteria for the common attribute (that is, skill level) that we want to match players on. You can use 3 different types of range criteria for Thresholds to fine-tune your Matches and achieve more precision when matching players with similar attributes:

* *Absolute* \- Match Players that fall between the specified minimum and maximum range of absolute values.

  **Example:** During the first Threshold period, players will only be matched when each have a skill level between the values of 19 and 21.
* *Relative* \- Find a match between two players where their values are no wider apart than the specified minimum and maximum values.

  **Example:** During the second Threshold period, if player 1 submits a [MatchmakingRequest](/API Documentation/Request API/Multiplayer/MatchmakingRequest.md) with a skill level of X, player 1 will only be matched to another player who has a skill level 3 greater than or 3 less than X.
* *Percentage* \- Similar to Relative and finds a match between players when their values are no wider apart than the specified minimum and maximum percentage values.

  **Example:** During the third Threshold period, if player 1 submits a *MatchmakingRequest* with a skill level of X, player 1 will only be matched to another player who has a skill level between 25 percent less than and 50 percent greater than X.


### Threshold Periods

You can use the *Period* value for a Threshold in your Match to specify how long you want to look for a match based on that Threshold's criteria.

We saw in the example that we can create multiple Threshold periods during one Match and for those Periods of time specify different Threshold types on which players will be matched - we had 3 Threshold Types, all with different Periods. Once the *MatchmakingRequest* is executed, if a match is not found in the first period, the following periods will continue subsequently to try to find a match until their duration has expired. By having a combination of longer and shorter Periods for the Thresholds, we can fine-tune our Match criteria to be stricter or more relaxed, while the duration of the Match progresses.

Our example showed how the use of 3 Thresholds types allows you to control the matching process performed by the portal such that you get a decreasing degree of matching precision as the matching process runs through the 30 second total matching period - *Absolute* matching for 10 seconds, *Relative* matching for the next 10 seconds, and *Percent* matching for the next 10 seconds.

### Accept Minimum Players

Selecting this for one of the Thresholds in your Match instructs the Match to match all the players it has currently found, as soon as the number of players found and matched is equal to the value in the *Min. Players* field. If enough players according to this value have not been found, the Match continues to find players in the next Threshold.

**Example:** Suppose our first Threshold, using *Absolute* type, was selected to *Accept Min Players*. *Min. Players* for *MULTI_MCH* is set at 2. Now suppose a player with skill level 20 issues a *MatchmakingRequest* using the *MULTI_MCH*. If 1 other matching player is found in the first 10 seconds - at, say, 4 seconds in with skill level 21 - then the Match would be made for these 2 players and the matchmaking process would cease after only 4 seconds had elapsed.

<q>**Note:** You can only apply *Accept Min. Players* to *one* Threshold in a Match. However, where there are multiple Thresholds, then *Accept Min. Players* will also be applied to any successive Thresholds used up to completion of the matchmaking process. So, in our current example, if the minimum of 2 matched players are not found in the first 10 seconds and during the *Absolute* Threshold period, but 2 matched players are found after 12 seconds and during the *Relative* Threshold period, the match will be made and the matchmaking process will cease.</q>

<q>**Remember!**  If *Accept Min. Players* is not selected for any Threshold, and there aren't enough players found in the Match to reach the *Max. Players* value, no Match will be found, even if there are more players than the *Min. Players* value.</q> 

### Multiplayer Matching Examples

Using the three Thresholds in the above *MULTI_MCH* example and for a 3-player context, here are some example scenarios to demonstrate just how the matching process works:

* **Scenario 1.** Players *1*, *2*, and *3* have skills of *20*, *15*, and *17* respectively. Each player submits a *MatchmakingRequest* in that order and each player's request is issued within player *1's* first Threshold period of 10 seconds. Players *1* and *3* would be matched based on the second Threshold which uses the Relative Match Type.

* **Scenario 2.** Players *1*, *2*, and *3* have skills of *20*, *15*, and *16* respectively. Each player submits a *MatchmakingRequest* in that order and each player's request is issued within player *1's* first Threshold period of 10 seconds. Players *2* and *3* would be matched based on the second Threshold which uses the Relative Match Type.

* **Scenario 3.** Players *1*, *2*, and *3* have skills of *20*, *15*, and *16* respectively. Player *1* submits a *MatchmakingRequest*. However, players *2* and *3* submit their requests later and during player *1's* *second* Threshold period of 20 seconds. Players *1* and *3* are matched based on the third Threshold which uses the Percent Match Type.



## Multiplayer Matching in the Test Harness

To match multiple Players, we will use the [MatchmakingRequest](/API Documentation/Request API/Multiplayer/MatchmakingRequest.md) in the *Test Harness*.  

*5.* In the *Test Harness*, authenticate 4 Players (in separate browser tabs) and have them each submit a *MatchmakingRequest* within 10 seconds so that all Players can attempt to match each other in their first threshold period.

Players *1*, *2*, *3* and *4* should have a skill of *16*, *21*, *19* and *22* respectively.

```
{
 "@class": ".MatchmakingRequest",
 "matchGroup": "group1",
 "matchShortCode": "MULTI_MCH",
 "skill": 16
}
```
```
{
 "@class": ".MatchmakingRequest",
 "matchGroup": "group1",
 "matchShortCode": "MULTI_MCH",
 "skill": 21
}
```
```
{
 "@class": ".MatchmakingRequest",
 "matchGroup": "group1",
 "matchShortCode": "MULTI_MCH",
 "skill": 19
}
```
```
{
 "@class": ".MatchmakingRequest",
 "matchGroup": "group1",
 "matchShortCode": "MULTI_MCH",
 "skill": 22
}
```

As you will notice, Players *2* and *3* will be matched almost immediately, because their skill values fall within the *first* (Absolute) threshold period.

Player 3 *MatchUpdatedMessage:*

```

{
  "@class": ".MatchUpdatedMessage",
  "addedPlayers": [
   "577679844ff544049a84c6dc"
  ],
  "gameId": 358380,
  "matchGroup": "group1",
  "matchShortCode": "MULTI_MCH",
  "messageId": "57767afd4ff544049a84d118",
  "notification": true,
  "participants": [
   {
    "displayName": "PLAYER_2",
    "externalIds": {},
    "id": "577679844ff544049a84c6cd",
    "online": true
   },
   {
    "displayName": "PLAYER_3",
    "externalIds": {},
    "id": "577679844ff544049a84c6dc",
    "online": true
   }
  ],
  "playerId": "577679844ff544049a84c6dc",
  "summary": "MatchUpdatedMessage"
}



```

Around 10 seconds later, Player *4* will also be added to the Match, who will be matched based on his skill value falling within the *second* (Relative) threshold period.  As each Player is added to the Match, both them and the existing Players on the Match receive a [MatchUpdatedMessage](/API Documentation/Message API/Multiplayer/MatchUpdatedMessage.md).

Player 3 *MatchUpdatedMessage:*

```

{
  "@class": ".MatchUpdatedMessage",
  "addedPlayers": [
   "577679844ff544049a84c6ec"
  ],
  "gameId": 358380,
  "matchGroup": "group1",
  "matchShortCode": "MULTI_MCH",
  "messageId": "57767b054ff544049a84d13c",
  "notification": true,
  "participants": [
   {
    "displayName": "PLAYER_2",
    "externalIds": {},
    "id": "577679844ff544049a84c6cd",
    "online": true
   },
   {
    "displayName": "PLAYER_3",
    "externalIds": {},
    "id": "577679844ff544049a84c6dc",
    "online": true
   },
   {
    "displayName": "PLAYER_4",
    "externalIds": {},
    "id": "577679844ff544049a84c6ec",
    "online": true
   }
  ],
  "playerId": "577679844ff544049a84c6dc",
  "summary": "MatchUpdatedMessage"
}


```


Finally, Player *1* will be added to the Match, who is matched based on his skill value falling within the *third* (Percent) threshold period.  This will result in a [MatchFoundMessage](/API Documentation/Message API/Multiplayer/MatchFoundMessage.md).


```


{
  "@class": ".MatchFoundMessage",
  "gameId": 358380,
  "matchGroup": "group1",
  "matchId": "57767b0f4ff544049a84d157",
  "matchShortCode": "MULTI_MCH",
  "messageId": "57767b0f4ff544049a84d168",
  "notification": true,
  "participants": [
   {
    "displayName": "PLAYER_2",
    "externalIds": {},
    "id": "577679844ff544049a84c6cd",
    "online": true,
    "peerId": 2
   },
   {
    "displayName": "PLAYER_1",
    "externalIds": {},
    "id": "577679844ff544049a84c6bf",
    "online": true,
    "peerId": 1
   },
   {
    "displayName": "PLAYER_3",
    "externalIds": {},
    "id": "577679844ff544049a84c6dc",
    "online": true,
    "peerId": 3
   },
   {
    "displayName": "PLAYER_4",
    "externalIds": {},
    "id": "577679844ff544049a84c6ec",
    "online": true,
    "peerId": 4
   }
  ],
  "playerId": "577679844ff544049a84c6dc",
  "summary": "MatchFoundMessage"
}

```


*6.* Repeat *Step 5*, but instead, change the skill value for Player *1* to be *12*. As Players *2, 3* and *4* are added to the Match, the average skill value in the Match increases and Player *1's* skill value will be too far away from the average value in the Match, even during the *third* (Percent) threshold period to match them.  A [MatchNotFoundMessage](/API Documentation/Message API/Multiplayer/MatchNotFoundMessage.md) message will be returned to all Players requesting a Match, including those already in the Match:



```
{
  "@class": ".MatchNotFoundMessage",
  "gameId": 358380,
  "matchGroup": "group1",
  "matchShortCode": "MULTI_MCH",
  "messageId": "57767bb64ff544049a84d6b3",
  "notification": true,
  "playerId": "577679844ff544049a84c6bf",
  "summary": "MatchNotFoundMessage"
}
```

As a result, no Match will be created. The Match we created earlier can be viewed using the [MatchDetailsRequest](/API Documentation/Request API/Multiplayer/MatchDetailsRequest.md). 

Here is the request submitted by Player *4*:

```
{
  "@class": ".MatchDetailsRequest",
 "matchId": "57767b0f4ff544049a84d157",
 "realtimeEnabled": false
}


```
And the *MatchDetailsResponse*:

```
{
  "@class": ".MatchDetailsResponse",
  "matchId": "57767b0f4ff544049a84d157",
  "opponents": [
   {
    "displayName": "PLAYER_2",
    "externalIds": {},
    "id": "577679844ff544049a84c6cd",
    "online": true,
    "peerId": 2
   },
   {
    "displayName": "PLAYER_1",
    "externalIds": {},
    "id": "577679844ff544049a84c6bf",
    "online": true,
    "peerId": 1
   },
   {
    "displayName": "PLAYER_3",
    "externalIds": {},
    "id": "577679844ff544049a84c6dc",
    "online": true,
    "peerId": 3
   }
  ],
  "peerId": 4,
  "playerId": "577679844ff544049a84c6ec"
}
```

### Cancelling a Match Request

*7. * To cancel an ongoing *MatchmakingRequest*, use the *action* parameter in the request with the value, *cancel*.

```
{
 "@class": ".MatchmakingRequest",
 "action": "cancel",
 "matchShortCode": "MULTI_MCH"
}
```

This will cancel a *MatchmakingRequest* that has not yet received any Match message.

## Using Drop In/Drop Out

In this type of Match, a Match is made in the normal way but the player list found for the Match doesn't remain fixed after the Match is made. Players that meet all of the matching criteria can enter or leave the Match.

Two constraints are imposed:
  * The number of players can change but cannot exceed the configured maximum number of players for the Match.
  * If all players drop out, then the Match is deleted.

<q>**Note:** The specified *minimum number of players* is applied for making the Match in the first place. However, after the Match has been made and during the Drop In/Drop Out period, player numbers *can fall below the minimum* and the Match will not be ended. This allows more players to drop in again and thus bring the number in the Match back up above the minimum.</q>

There are two important settings for this type of Match:
* *Player disconnect delay in seconds* \- The number of seconds after a Match is found before a player in the Match who disconnects is removed from the Match. If you do not enter a value or enter zero, then a player in the Match who disconnects is removed instantly.
* *Expire in seconds* \- The number of seconds after a Match is made that players can drop in or drop out. If you do not enter a value or enter zero, the drop in/drop out period for the Match doesn't expire.

![](img/HowToMatchPlayers/8.png)

Here, we've edited our earlier multiplayer Match example and enabled Drop In/Drop Out:
* Any player in the Match who disconnects will be removed from the Match after 15 seconds. If the player reconnects within 15 seconds, they will be retained in the Match.
* Matched players can drop in and drop out of the Match for up to 5 minutes after the Match was originally made.

## Manually Matching

You might want the GameSparks portal to process all the matching criteria you have built into a Match configuration, produce a list of players that meet those criteria, but not have the portal complete the Match in the normal way. Instead, you want to use your own custom mechanism to complete the Match and based on the player list found for the Match. You can use Manually Matching for this sort of case and you must select to *Manually match players*:

![](img/HowToMatchPlayers/9.png)

To build a custom completion mechanism for a Match, you will typically use *FindPendingMatchesRequest* and *JoinPendingMatchRequest*.

<q>**Possible Availability Lag!** If you use manual matching, an "availabilty lag" might occur and prevent the Match being made. This would happen in cases where the matching process has presented the results for players meeting the matching criteria, but by the time your custom mechanism actually completes the Match one or more of the matched players is no longer available and the Match will not go through.</q>
