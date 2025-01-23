---
tags:
  - Unity
  - Script
---
- Interface for Game Managers
```cs
public interface IGameManager
{
    ManagerStatus status { get; }

    void Startup(NetworkService service);
}

```