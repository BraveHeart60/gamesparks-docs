title: DropTeamRequest
link: https://docs.gamesparks.net/documentation/request-api/teams-request-api/dropteamrequest
author: GameSparks
description: 
post_id: 4389
created: 2014/08/04 15:33:04
created_gmt: 2014/08/04 15:33:04
comment_status: open
post_name: dropteamrequest
status: publish
post_type: post

<!--Allows a player to drop a team. -->

# DropTeamRequest

Allows a player to drop a team.

#### Parameters

Name : TypeRequiredDescription

ownerId:string
No

The team owner to find, used in combination with teamType. If not supplied the current players id will be used

requestId:string
No

The SDK adds a requestId to all requests, this is used to match responses from the websocket

teamId:string
No

The teamId to find (may be null if teamType supplied)

teamType:string
No

The teamType to find, used in combination with the current player, or the player defined by ownerId

#### Errors

NameValueDescription

teamId|teamType
REQUIRED

Both teamId and teamType have not been provided

team
INVALID

The teamId or the teamType do not match an existing team

team
NOT_MEMBER

The current player is not a mamber of the team they are requesting to leave

teamType&&ownerId;
NOT_UNIQUE

The ownerId / teamType combination has multiple teams related to it

  


## Example Request
    
    
    {
      "@class" : ".DropTeamRequest",
      "ownerId" : "12345",
      "teamId" : "12345",
      "teamType" : "SQUAD"
    }

## Example Response
    
    
    {
      "@class" : ".DropTeamResponse",
      "members" : [ {
        "achievements" : [ "..." ],
        "displayName" : "...",
        "externalIds" : "...",
        "id" : "...",
        "online" : false,
        "scriptData" : { },
        "virtualGoods" : [ "..." ]
      } ],
      "owner" : {
        "achievements" : [ "..." ],
        "displayName" : "...",
        "externalIds" : "...",
        "id" : "...",
        "online" : false,
        "scriptData" : { },
        "virtualGoods" : [ "..." ]
      },
      "scriptData" : { },
      "teamId" : "...",
      "teamType" : "..."
    }