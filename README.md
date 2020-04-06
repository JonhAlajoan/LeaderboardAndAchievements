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

# Usage - SteamLeaderboard.cs

## Simple usage
If you want to just generate a leaderboard without too much of a hassle, after filling the editor parts (on image below) put the LeaderboardTarget.cs script on a canvas (that'll be the leaderboard parent) and call the coroutine below. If you follow the image, it'll create the leaderboard recovering the information from the steam API site leaderboard called "db_teste_board", showing 5 entries from the global leaderboard.

```C#
SteamLeaderboard.InstantiateLeaderboard(this)
```

<p align="center">
  <img width="444" height="467" src="https://github.com/bratus/LeaderboardAndAchievements/blob/master/Icons/ImageLeaderboard.png">
</p>

Attributes:
- Leaderboard name: The leaderboard name from steam API web page;
- Leaderboard cell prefab: Prefab that contains each "cell" of the leaderboard, **MUST** contain:
  + An Image GameObject
  + Two Text GameObjects (First one will be the player name, The second one will be the player score)
  + **It is important to follow this model, otherwise there'll be problems on lines 270-272**
- Leaderboard starting range: The initial range that you want to get for your leaderboard. On common cases, this will be 0, but for instance, if you use the requestType 
------------

+ SteamLeaderboard.cs
  + SteamLeaderboard.InstantiateLeaderboard(MonoBehaviour _coroutineStart);
  + SteamLeaderboard.FindLeaderboard();
  + SteamLeaderboard.DownloadLeaderboardEntries();
  + SteamLeaderboard.UseDownloadedEntries(); 
  + SteamLeaderboard.UpdateScore();
