---
tags:
  - Unity
  - Script
---
- Raycasting for a player shooter connected to the camera. Also locks the mouse produces a point for aiming and spheres to show where the hit occurred, targets will react to being hit
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;

public class RayShooter : MonoBehaviour
{
    private Camera cam;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        cam = GetComponent<Camera>();

        // Hide the mouse cursor at the centre of the screen
        Cursor.lockState = CursorLockMode.Locked;
        Cursor.visible = false;
    }

    // Update is called once per frame
    void Update()
    {
        // Toggle mouse movement
        if (Input.GetKeyDown(KeyCode.L))
        {
            Cursor.visible = !Cursor.visible;
            Cursor.lockState = Cursor.visible ? CursorLockMode.None : CursorLockMode.Locked;
        }
        
        // Respond to the left (first) mouse button
        // Check that GUI isn't being used
        if (Input.GetMouseButtonDown(0) && !EventSystem.current.IsPointerOverGameObject())
        {
            Vector3 point = new Vector3(cam.pixelWidth / 2, cam.pixelHeight / 2, 0);
            // Create the ray at that position
            Ray ray = cam.ScreenPointToRay(point);
            RaycastHit hit;
            // Raycast fills a referenced variable with information
            if (Physics.Raycast(ray, out hit))
            {
                // Retrieve the object the ray hit
                GameObject hitObject = hit.transform.gameObject;
                ReactiveTarget target = hitObject.GetComponent<ReactiveTarget>();
                // Check for ReactiveTarget component on the object
                if (target != null)
                {
                    target.ReactToHit();
                    Messenger.Broadcast(GameEvent.ENEMY_HIT);
                }
                else
                {
                    // Launch a coroutine in response to a hit
                    StartCoroutine(SphereIndicator(hit.point));
                }
            }
        } 
    }

    // Uses the basic built-in UI
    void OnGUI()
    {
        int size = 12;
        float posX = cam.pixelWidth / 2 - size / 4;
        float posY = cam.pixelHeight / 2 - size / 2;
        // Displays text onscreen
        GUI.Label(new Rect(posX, posY, size, size), "*");
    }

    // Note, coroutines use IEnumerator functions
    private IEnumerator SphereIndicator(Vector3 pos)
    {
        GameObject sphere = GameObject.CreatePrimitive(PrimitiveType.Sphere);
        sphere.transform.position = pos;

        // Yield tells coroutines where to pause
        yield return new WaitForSeconds(1);

        // Remove this gameObject and clear its memory
        Destroy(sphere);
    }
}
```

^9283b7
