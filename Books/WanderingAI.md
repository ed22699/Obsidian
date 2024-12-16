---
tags:
  - Unity
  - Script
---
- Very basic AI which walks around changing direction when a wall is near and firing when a player is in its path
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class WanderingAi : MonoBehaviour
{
    [SerializeField] GameObject fireballPrefab;
    private GameObject fireball;
    public float speed = 3.0f;

    public float obstacleRange = 5.0f;
    private bool isAlive;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        isAlive = true;
    }

    // Update is called once per frame
    void Update()
    {
        if (isAlive)
        {
            transform.Translate(0, 0, speed * Time.deltaTime);
            // Ray pointing in same direction as character
            Ray ray = new Ray(transform.position, transform.forward);
            RaycastHit hit;
            // Perform raycasting with a circular volume around the ray
            if (Physics.SphereCast(ray, 0.75f, out hit))
            {
                GameObject hitObject = hit.transform.gameObject;
                // Player detected
                if (hitObject.GetComponent<PlayerCharacter>())
                {
                    if (fireball == null)
                    {
                        fireball = Instantiate(fireballPrefab) as GameObject;
                        // place fireball in front of the enemy and point in the same direction
                        fireball.transform.position = transform.TransformPoint(Vector3.forward * 1.5f);
                        fireball.transform.rotation = transform.rotation;
                    }
                }
                else if (hit.distance < obstacleRange)
                {
                    float angle = Random.Range(-110, 110);
                    transform.Rotate(0, angle, 0);
                }
            }
        }
    }

    public void SetAlive(bool alive)
    {
        isAlive = alive;
    }
}
```