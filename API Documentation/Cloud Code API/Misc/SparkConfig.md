# SparkConfig

Contains configuration information for the game


## getStage
_signature_ getStage()</p>
_returns_ string</p>
<b>validity</b> All Scripts
Returns the stage (preview or live) the game is running on

## getApiKey
_signature_ getApiKey()</p>
_returns_ string</p>
<b>validity</b> All Scripts
Returns the apiKey of the game

## getVirtualGoods
_signature_ getVirtualGoods()</p>
_returns_ JSON</p>
<b>validity</b> All Scripts
Returns a list of the Virtual Goods configured against the game

## getVirtualGood
_signature_ getVirtualGood(string shortCode)</p>
_returns_ [SparkVirtualGood](../Misc/SparkVirtualGood.md)</p>
<b>validity</b> All Scripts
Returns the virtual good with the supplied short code

## getAchievements
_signature_ getAchievements()</p>
_returns_ JSON</p>
<b>validity</b> All Scripts
Returns a list of the Achievements configured against the game

## getAchievement
_signature_ getAchievement(string shortCode)</p>
_returns_ [SparkAchievement](../Misc/SparkAchievement.md)</p>
<b>validity</b> All Scripts
Returns the achievement with the supplied short code

## getSegments
_signature_ getSegments()</p>
_returns_ JSON</p>
<b>validity</b> All Scripts
Returns a list of the Segments configured against the game

## getSegment
_signature_ getSegment(string shortCode)</p>
_returns_ [SparkSegmentType](../Misc/SparkSegmentType.md)</p>
<b>validity</b> All Scripts
Returns the segment with the supplied short code

## getTeams
_signature_ getTeams()</p>
_returns_ JSON</p>
<b>validity</b> All Scripts
Returns a list of the Teams configured against the game

## getTeam
_signature_ getTeam(string shortCode)</p>
_returns_ [SparkTeamType](../Misc/SparkTeamType.md)</p>
<b>validity</b> All Scripts
Returns the team with the supplied short code

## getChallenges
_signature_ getChallenges()</p>
_returns_ JSON</p>
<b>validity</b> All Scripts
Returns a list of the Challenges configured against the game

## getChallenge
_signature_ getChallenge(string shortCode)</p>
_returns_ [SparkChallengeType](../Misc/SparkChallengeType.md)</p>
<b>validity</b> All Scripts
Returns the challenge with the supplied short code

## getDownloadable
_signature_ getDownloadable(string shortCode)</p>
_returns_ [SparkDownloadable](../Misc/SparkDownloadable.md)</p>
<b>validity</b> All Scripts
Returns the downloadable with the supplied short code

## getDownloadables
_signature_ getDownloadables()</p>
_returns_ [SparkDownloadable](../Misc/SparkDownloadable.md)[]</p>
<b>validity</b> All Scripts
Returns a list of all the downloadables configured for this game

