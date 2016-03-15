
# LeaveTeamRequest


Allows a player to leave a team.


## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
ownerId | No | string | The team owner to find, used in combination with teamType. If not supplied the current players id will be used
teamId | No | string | The teamId to find (may be null if teamType supplied)
teamType | No | string | The teamType to find, used in combination with the current player, or the player defined by ownerId

## Response Parameters


A response to a player leaving a team

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
team | [Team](#team) | A JSON object representing the team

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### Team

A nested object that represents the team.

Parameter | Type | Description
--------- | ---- | -----------
members | [Player[]](#player) | The team members
owner | [Player](#player) | A summary of the owner
teamId | string | The Id of the team
teamName | string | The team name
teamType | string | The team type

### Player

A nested object that represents a player.

Parameter | Type | Description
--------- | ---- | -----------
achievements | string[] | The achievements of the Player
displayName | string | The display name of the Player
externalIds | JSON | The external Id's of the Player
id | string | The id of the Player
online | boolean | The online status of the Player
scriptData | JSON | The script data of the Player
virtualGoods | string[] | The virtual goods of the Player

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
teamId&#124;teamType | REQUIRED | Both teamId and teamType have not been provided
team | INVALID | The teamId or the teamType do not match an existing team
team | CANNOT_LEAVE_OWNED_TEAM | The current player is trying to leave a team they own.
team | NOT_MEMBER | The current player is not a mamber of the team they are requesting to leave
teamType&&ownerId | NOT_UNIQUE | The ownerId / teamType combination has multiple teams related to it

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new LeaveTeamRequest()
		.SetOwnerId(ownerId)
		.SetTeamId(teamId)
		.SetTeamType(teamType)
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
		var team = response.Team; 
		});

```

### ActionScript 3
```actionscript
	import com.gamesparks.*;
	import com.gamesparks.api.requests.*;
	import com.gamesparks.api.responses.*;
	import com.gamesparks.api.types.*;
	...
	
	gs.getRequestBuilder()
	    .createLeaveTeamRequest()
		.setOwnerId(ownerId)
		.setTeamId(teamId)
		.setTeamType(teamType)
		.send(function(response:com.gamesparks.api.responses.LeaveTeamResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var team:Team = response.getTeam(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSLeaveTeamRequest* request = [[GSLeaveTeamRequest alloc] init];
	[request setOwnerId:ownerId;
	[request setTeamId:teamId;
	[request setTeamType:teamType;
	[request setCallback:^ (GSLeaveTeamResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
	GSTeam* team = [response getTeam]; 
	}];
	[gs send:request];

```

### C++
```cpp

	#include <GameSparks/generated/GSRequests.h>
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Responses;
	using namespace GameSparks::Api::Requests;
	...
	
	void LeaveTeamRequest_Response(GS& gsInstance, const LeaveTeamResponse& response) {
	GSData scriptData = response.getScriptData(); 
	Types::Team* team = response.getTeam(); 
	}
	......
	
	LeaveTeamRequest request(gsInstance);
	request.SetOwnerId(ownerId)
	request.SetTeamId(teamId)
	request.SetTeamType(teamType)
	request.Send(LeaveTeamRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.LeaveTeamRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.LeaveTeamResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createLeaveTeamRequest()
	.setOwnerId(ownerId)
	.setTeamId(teamId)
	.setTeamType(teamType)
	.send(new GSEventListener<LeaveTeamResponse>() {
		@Override
		public void onEvent(LeaveTeamResponse response) {
			GSData scriptData = response.getScriptData(); 
			Team team = response.getTeam(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.LeaveTeamRequest();
	request.ownerId = ...;
	request.teamId = ...;
	request.teamType = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
var team = response.team; 
```


