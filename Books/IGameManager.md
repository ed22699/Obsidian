---
tags:
  - Unity
  - Script
---
- Interface for managers
```cs
public interface IGameManager
{
    ManagerStatus status { get; }

    void Startup();
}

```