---
tags:
  - Unity
  - Script
---
- Script that moves a 3D player around, can jump, fall/slide down steep surfaces, has animations
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(CharacterController))]
public class RelativeMovement : MonoBehaviour
{
    public float rotSpeed = 15.0f;
    public float moveSpeed = 6.0f;
    public float jumpSpeed = 15.0f;
    public float gravity = -9.8f;
    public float terminalVelocity = -10.0f;
    public float minFall = -1.5f;

    private CharacterController charController;
    private float vertSpeed;
    private ControllerColliderHit contact;
    private Animator animator;
    
    [SerializeField] Transform target;

    void Start()
    {
        charController = GetComponent<CharacterController>();
        vertSpeed = minFall;
        animator = GetComponent<Animator>();
    }
    
    // Update is called once per frame
    void Update()
    {
        // Start with vector (0,0,0) and add movement components progressively 
        Vector3 movement = Vector3.zero;
        float horInput = Input.GetAxis("Horizontal");
        float vertInput = Input.GetAxis("Vertical");
        // Handle movmeent only while arrow keys are pressed
        if (horInput != 0 || vertInput != 0)
        {
            Vector3 right = target.right;
            // Calculate the player's forward direction by using the cross product of the target's right direction
            Vector3 forward = Vector3.Cross(right, Vector3.up);
            // Add together the input in each directio to get the combined movement vector
            movement = (right * horInput) + (forward * vertInput);
            // The facing directions are magnitude 1, so multiply with the desired speed value
            movement *= moveSpeed;
            // Limit diagonal movemnt to the same speed as movement along an axis
            movement = Vector3.ClampMagnitude(movement, moveSpeed);
            // LookRotation() calculates a quaternion facing in that direction
            Quaternion direction = Quaternion.LookRotation(movement);
            transform.rotation = Quaternion.Lerp(transform.rotation, direction, rotSpeed * Time.deltaTime);
        }

        animator.SetFloat("Speed", movement.sqrMagnitude);
        bool hitGround = false;
        RaycastHit hit;
        // Check if the player is falling
        if (vertSpeed < 0 && Physics.Raycast(transform.position, Vector3.down, out hit))
        {
            // Distance to check against don't really understand the 0.4 comes from
            float check = (charController.height + charController.radius) / 0.4f;
            hitGround = hit.distance <= check;
        }

        // Check if controller is on ground
        if (hitGround)
        {
            // React to the jump button while on the ground
            if (Input.GetButtonDown("Jump"))
            {
                vertSpeed = jumpSpeed;
            }
            // If not one ground apply gravity until terminal velocity reached
            else
            {
                vertSpeed = minFall;
                animator.SetBool("Jumping", false);
            }
        }
        else
        {
            vertSpeed += gravity * 5 * Time.deltaTime;
            if (vertSpeed < terminalVelocity)
            {
                vertSpeed = terminalVelocity;
            }

            // Don't trigger this value right at the beginning of the level
            if (contact != null)
            {
                animator.SetBool("Jumping", true);
            }

            // Raycasting didn't detect ground, but capsule is touching the ground
            if (charController.isGrounded)
            {
                // Respond slightly differently depending on whether the character is facing the contact point
                if (Vector3.Dot(movement, contact.normal) < 0)
                {
                    movement = contact.normal * moveSpeed;
                }
                else
                {
                    movement += contact.normal * moveSpeed;
                }
            }
        }

        movement.y = vertSpeed;
        // Always multiply movements by deltaTime to make them frame-rate independent
        movement *= Time.deltaTime;
        charController.Move(movement);
    }

    // Store the collision data in the callback when a collision is detected
    void OnControllerColliderHit(ControllerColliderHit hit)
    {
        contact = hit;
    }
}

```