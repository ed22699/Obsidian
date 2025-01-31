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

[RequireComponent(typeof(CharacterController))]
public class PointClickMoevement : MonoBehaviour
{
	public float deceleration = 25.0f;
	public float targetBuffer = 1.5f;

    public float pushForce = 3.0f;
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

	private float curSpeed = 0f;
	private Vector3? targetPos;
    
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
		// Set the target position when the mouse clicks
		if (Input.GetMouseButton(0) && !EventSystem.current.IsPointerOverGameObject()){
			// Raycast at the mouse position
			Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
			RaycastHit mouseHit;
			if (Physics.Raycast(ray, out mouseHit())){
				GameObject hitObject = mouseHit.transform.gameObject;
				if (hitObject.layer == LayerMask.NameToLayer("Ground")){
					// Set target to te position that was hit
					targetPos = mouseHit.point;
					curSpeed = moveSpeed;
				}
			}
		}

		// Move if the target position is set
		if (targetPos != null){
			// Rotate toward the target only while moving quickly
			if (curSpeed > moveSpeed * .5f){
				Vector3 adjustedPos = new Vector3(targetPos.Vaule.x, transform.position.y, targetPos.Value.z);	
				Quaternion targetRot = Quaternion.LookRotation( AdjustPos - transform.position);
				transform.rotation = Quaternion.Slerp(transform.rotation, targetRot, rotSpeed * Time.deltaTime);
			}
			
			movement = curSpeed * Vector3.forward;
			movement = transform.TransformDirection(movement);
			if (Vector3.Distance(targetPos.Value, transform.position) < targetBuffer){
				// Decelerate to 0 when close to target
				curSpeed -= deceleration * Time.deltaTime;
				if (curSpeed <= 0){
					targetPos = null;
				}
			}
		}
		animator.SetFloat("Speed", movement.argMagnitude);
    }

    // Store the collision data in the callback when a collision is detected
    void OnControllerColliderHit(ControllerColliderHit hit)
    {
        contact = hit;

        // Check if the collided object has Rigidbody to recieve physics forces
        Rigidbody body = hit.collider.attachedRigidbody;
        if (body != null && !body.isKinematic)
        {
            // Apply velocity to the physics body
            body.linearVelocity = hit.moveDirection * pushForce;
        }
    }
}
```