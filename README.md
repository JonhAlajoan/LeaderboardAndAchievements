![](https://github.com/bratus/LeaderboardAndAchievements/blob/master/Icons/Icon.png)


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
If you want to just generate a leaderboard without too much of a hassle, after filling the editor parts (
+ SteamLeaderboard.cs
  + SteamLeaderboard.InstantiateLeaderboard(MonoBehaviour _coroutineStart);
  + SteamLeaderboard.FindLeaderboard();
  + SteamLeaderboard.DownloadLeaderboardEntries();
  + SteamLeaderboard.UseDownloadedEntries(); 
  + SteamLeaderboard.UpdateScore();
