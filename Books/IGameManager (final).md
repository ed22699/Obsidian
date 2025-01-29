---
tags:
  - Unity
  - Script
---
- Description
```cs
public interface IGameManager
{
    ManagerStatus status { get; }

    void Startup(NetworkService service);
}
```