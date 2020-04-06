<p align="center">
  <img width="512" height="256" src="https://github.com/bratus/LeaderboardAndAchievements/blob/master/Icons/Icon.png">
</p>

Hello, this is the basic documentation for bratus leaderboard and achievements for steamworks that can be found at: https:linkDoAssetStore

# Features

### Features - Leaderboard
- Retrieve leaderboard entries by selected method
- Updating leaderboard by selected method
- Get images for each player entry
- Simple implementation that can be modified for custom necessities
------------
### Features - Achievements

- Reconcile achievements for easy administration of unlockables
- Get the icons of the achievements for menu uses
- Unlock or lock achievements with one function
- Update and retrieve stats for achievement progress (only work with ints
- Clear achievements for testing 
------------
# Usage
The library has 3 main scripts:
- SteamLeaderboard.cs
- SteamLeaderboardTarget.cs
- SteamAchievements.cs

Their usage will be explained below, but to use any of the scripts first you'll need to configure your steamAppID. To do this simply create a .txt file called _"steam_appid"_ at the root folder of your project (the folder before assets). After this, open the file and fill it only with the SteamAppId given to your game. Once you've done this, open the script  _SteamManager.cs_ and at line 86, put your AppID like shown on the image:
<p align="center">
  <img width="807" height="711" src="https://github.com/bratus/LeaderboardAndAchievements/blob/master/Icons/AppIDExample.png">
</p>

If you succeeded at configuring your SteamAppID, you only need to have your steam open and you're should be good to go. To use any of the scripts on this asset, you'll need to put above your script:
```C#
using BratusSteamLibraries;
```
------------

# Usage - SteamLeaderboard
## Attributes and simple usage
<p align="center">
  <img width="444" height="467" src="https://github.com/bratus/LeaderboardAndAchievements/blob/master/Icons/ImageLeaderboard.png">
</p>

- **Leaderboard name:** The leaderboard name from steam API web page;
- **Leaderboard cell prefab:** Prefab that contains each "cell" of the leaderboard, **MUST** contain:
  + An Image GameObject
  + Two Text GameObjects (First one will be the player name, The second one will be the player score)
  + **It is important to follow this model, otherwise there'll be problems on lines 270-272**
- **Leaderboard starting range:** The starting range on how many entries will be downloaded
- **Leaderboard ending range:** The ending range on how many entries will be downloaded
- **Distance between each cell:** The distance between each cell on your leaderboard. Depending on how your leaderboard is made, you may need to change the "-" for a "+" on line 260
- **Upload score method:** How the score will be uploaded
  + ELeaderboardUploadScoreMethodKeepBest = Keeps the best scores, and normally will be the one used
  + ELeaderboardUploadScoreMethodForceUpdate = Update the score as best, independent of the score
- **Request type:** How the leaderboard will be handled
  + k_ELeaderboardDataRequestGlobal = Requests the data from all results
  + k_ELeaderboardDataRequestFriends = Requests the data from all your steam friends
  + k_ELeaderboardDataRequestGlobalAroundUser = Request from global data, but the range will be around the user. Eg: if the range is -3,3 it'll return the 3 results before and after the player
  + k_ELeaderboardDataRequestUsers = Can not be used, specified on Steam APi.
  
If you want to just generate a leaderboard without too much of a hassle, first create a leaderboard at: "https://partner.steamgames.com/apps/leaderboards/yourSteamAppID". after this, fill the editor parts (on image above) put the **LeaderboardTarget.cs** script on a canvas (that'll be the leaderboard parent) and call the coroutine below. If you follow the image, it'll create the leaderboard recovering the information from the steam API site leaderboard called "db_teste_board", showing 5 entries from the global leaderboard.

```C#
SteamLeaderboard.InstantiateLeaderboard(this)
```
------------
## Methods
+ **SteamLeaderboard.InstantiateLeaderboard(MonoBehaviour _coroutineStart):**
  +  Creates the leaderboard on the m_leaderboardTarget gameObject. "this" is the normal parameter, it'll get the instance of the object monobehaviour to play the coroutine.
+ **SteamLeaderboard.FindLeaderboard():**
  + this method is used to search the leaderboard by name with a SteamAPICall
+ **SteamLeaderboard.DownloadLeaderboardEntries():**
  + This method download the leaderboard entries from the set range
+ **SteamLeaderboard.UseDownloadedEntries():**
  + This method uses the downloaded entries to create a list of players. If you want to modify the code, the "for" index will be used as the index to get the entries to be modified
+ **SteamLeaderboard.UpdateScore(int _score):**
  + Update score into the Steam leaderboards The method is bool so you can use it as a condition.
+ **public static Sprite FetchAvatar(CSteamID _steamID):**
  + fetches the avatar from given _steamID._ Normally you can get this id using 
  ```C#
  SteamFriends.GetFriendPersonaName(_LeaderboardEntry.m_steamIDUser)
  ```
-------------
# Usage - SteamAchievements 
## Attributes and simple usage
<p align="center">
  <img width="450" height="63" src="https://github.com/bratus/LeaderboardAndAchievements/blob/master/Icons/exampleAchievements.png">
</p>
**Quantity of achievements:** The total quantity of achievements. If you registered 100 achievements on your game, the total quantity of achievements that you'll fill the attribute is _99_ because it counts from 0. This will be used to create the list of achievements to be used.
**Pattern of achievement names:** The achievement must be named at the Steam Achievements web page as: "ACHIEVEMENT_XX" where x is the actual number of the achievement. For instance, if you have 5 achievements they must be named: "ACHIEVEMENT_00", "ACHIEVEMENT_01", "ACHIEVEMENT_02", ""ACHIEVEMENT_03", "ACHIEVEMENT_04".
**Pattern of Steam Stats names:** If your achievements use stats (10 games won, for instance) the name of the stat must follow the rules above, but it needs to add the "_STAT_" after the achievement name. For instance, if your achievement name "ACHIEVEMENT_12" needs a stat, the stat must be an int and named: "ACHIVEMENT_12_STAT".
**TIP:** Before changing the achievements, you need to publish it on steam. If you change but don't publish your achievements, it won't work.

If you want to just unlock an achievement, after creating the achievements on the steam web page: "https://partner.steamgames.com/apps/achievements/yourSteamAPPID", use the following code to unlock the achievement:
  ```C#
 SteamAchievements.UnlockSteamAchievement("nameOfAchievement");
  ```
If you want to update a Steam Stat, after creating a stat and naming as the patterns above at: "https://partner.steamgames.com/apps/stats/yourSteamAPPId", use the code below:
  ```C#
  //10 is the steam state value that i'm updating
 SteamAchievements.UpdateSteamStat("nameOfAchievement", 10);
  ```


