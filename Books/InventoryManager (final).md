---
tags:
  - Unity
  - Script
---
- Description
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InventoryManager : MonoBehaviour, IGameManager
{
	private Dictionary<string, int> items;
	private NetworkService network;

    public ManagerStatus status { get; private set; }

	public string equippedItem {get; private set;}

    public void Startup(NetworkService service)
    {
        // Any long-running startup tasks go here
        Debug.Log("Inventory manager starting...");
		items = new Dictionary<string, int>();
		network = service;
        // For long running tasks use stats initializing instead
        status = ManagerStatus.Started;
    }
	
	private void DisplayItems()
	{
		string itemDisplay = "Items: ";
		foreach (KeyValuePair<string, int> item in items)
		{
			itemDisplay += item.Key + "(" + item.Value + ") ";
		}
		Debug.Log(itemDisplay);
	}

	// Other scripts can't manupulate the item list directly but can call this
	public void AddItem(string name)
	{
		if (items.ContainsKey(name))
		{
			items[name] += 1;
		}
		else
		{
			items[name] = 1;
		}
		DisplayItems();
	}

	// Returns list of dictionary keys
	public List<string> GetItemList()
	{
		List<string> list = new List<string>(items.Keys);
		return list;
	}

	// Returns how many of that item are in the inventory
	public int GetItemCount(string name)
	{
		if (items.ContainsKey(name))
		{
			return items[name];
		}
		return 0;
	}

	public bool EquipItem(string name)
	{
		if (items.ContainsKey(name) && equippedItem != name)
		{
			equippedItem = name;
			Debug.Log($"Equipped {name}");
			return true;
		}

		equippedItem = null;
		Debug.Log("Unequipped");
		return false;
	}

	public bool ConsumeItem(string name)
	{
		// Check if item in inventory
		if (items.ContainsKey(name))
		{
			items[name]--;
			// Remove entry if count goes to 0
			if (items[name] == 0) 
			{
				items.Remove(name);
			}
		}
		// Response if that item isn't in inventory
		else
		{
			Debug.Log($"Cannot consume {name}");
			return false;
		}

		DisplayItems();
		return true;
	}
}
```