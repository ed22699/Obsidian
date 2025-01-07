---
tags:
  - Unity
  - Script
---
- Movement for a player of a platformer game
	- has animated movement
	- can move side to side and jump
		- only jumps when connected to floor
	- gravity is turned off when idle on a platform, this means player doesn't slide on slopes
	- player attaches to moving platforms
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlatformerPlayer : MonoBehaviour
{
    private Animator anim;
    private BoxCollider2D box;
    private Rigidbody2D body;
    public float speed = 4.5f;
    public float jumpForce = 12.0f;

    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        body = GetComponent<Rigidbody2D>();
        anim = GetComponent<Animator>();
        box = GetComponent<BoxCollider2D>();
    }

    // Update is called once per frame
    void Update()
    {
        float deltaX = Input.GetAxis("Horizontal") * speed;
        // Setting only horizontal movement
        Vector2 movement = new Vector2(deltaX, body.linearVelocity.y);
        body.linearVelocity = movement;

        Vector3 max = box.bounds.max;
        Vector3 min = box.bounds.min;
        // Check below the collider's min Y values
        Vector2 corner1 = new Vector2(max.x, min.y - .1f);
        Vector2 corner2 = new Vector2(min.x, min.y - .2f);
        Collider2D hit = Physics2D.OverlapArea(corner1, corner2);

        bool grounded = false;
        // If collider was detected under the player
        if (hit != null)
        {
            grounded = true;
        }

        // Check both on ground and not moving when turning off gravity
        body.gravityScale = (grounded && Mathf.Approximately(deltaX, 0)) ? 0 : 1;
        
        // Add force when spacebar pressed
        if (grounded && Input.GetKeyDown(KeyCode.Space))
        {
            body.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        }

        MovingPlatform platform = null;
        if (hit != null)
        {
            // Check whether the platform under the player is a moving platform
            platform = hit.GetComponent<MovingPlatform>();
        }

        // Default scale 1 is not on moving platform
        Vector3 pScale = Vector3.one;
        
        // Either attach to the platform or clear transform.parent
        if (platform != null)
        {
            transform.parent = platform.transform;
            pScale = platform.transform.localScale;
        }
        else
        {
            transform.parent = null;
        }
        // Speed is greater than zero even if velocity is negative
        anim.SetFloat("speed", Mathf.Abs(deltaX));

        // Floats aren't exact so compare with approximately
        if (!Mathf.Approximately(deltaX, 0))
        {
            // When moving, scale positive or negative 1 to face right or left
            transform.localScale = new Vector3(Mathf.Sign(deltaX) / pScale.x, 1/pScale.y, 1);
        }
    }
}
```