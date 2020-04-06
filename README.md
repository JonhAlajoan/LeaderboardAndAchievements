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

Their usage will be explained below, but to use any of the scripts first you'll need to put:
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
  
If you want to just generate a leaderboard without too much of a hassle, after filling the editor parts (on image above) put the LeaderboardTarget.cs script on a canvas (that'll be the leaderboard parent) and call the coroutine below. If you follow the image, it'll create the leaderboard recovering the information from the steam API site leaderboard called "db_teste_board", showing 5 entries from the global leaderboard.

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
  +
