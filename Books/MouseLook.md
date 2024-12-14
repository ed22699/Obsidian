---
tags:
  - Unity
  - Script
---
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MouseLook : MonoBehaviour
{
    public enum RotationAxes
    {
        MouseXAndY = 0,
        MouseX = 1,
        MouseY = 2
    }
    public RotationAxes axes = RotationAxes.MouseXAndY;

    // Sensitivities
    public float sensitivityHor = 9.0f;
    public float sensitivityVer = 9.0f;

    // Limits for looking up and down
    public float minimumVer = -45.0f;
    public float maximumVer = 45.0f;

    private float verticalRot = 0;
    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // Ensures environment in simulation does not affect player rotation
        Rigidbody body = GetComponent<Rigidbody>();
        if (body != null)
        {
            body.freezeRotation = true;
        }
    }

    // Update is called once per frame
    void Update()
    {
        if (axes == RotationAxes.MouseX)
        {
            // horizontal rotation
            var horRotation = Input.GetAxis("Mouse X") * sensitivityHor;
            transform.Rotate(0, horRotation, 0);
        } 
        else if (axes == RotationAxes.MouseY)
        {
            // vertical rotation
            verticalRot -= Input.GetAxis("Mouse Y") * sensitivityVer;
            verticalRot = Mathf.Clamp(verticalRot, minimumVer, maximumVer);
            float horizontalRot = transform.localEulerAngles.y;
            transform.localEulerAngles = new Vector3(verticalRot, horizontalRot, 0);
        }
        else
        {
            // both horizontal and vertical roation
            verticalRot -= Input.GetAxis("Mouse Y") * sensitivityVer;
            verticalRot = Mathf.Clamp(verticalRot, minimumVer, maximumVer);

            float delta = Input.GetAxis("Mouse X") * sensitivityHor;
            float horizontalRot = transform.localEulerAngles.y + delta;
            // This is the prefered method for incrementing with limit
            transform.localEulerAngles = new Vector3(verticalRot, horizontalRot, 0);
        }
    }
}
```