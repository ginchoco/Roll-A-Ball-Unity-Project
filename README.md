# Roll-A-Ball-Unity-Project
Worked with a beginner tutorial in Unity to learn how to make a very basic game setup working with assets, game objects, pre fabs, and scripting.

___________________________________________________________________________________________________
***Camera Controller Script***
___________________________________________________________________________________________________
    // Gaby Inchoco
    // Volumetric Cinema Pre-Assignment
    // 9/8/2019
    // Camera Controller Script       

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;

    // Controls the positioning of the main camera so that it will
    // be positioned consistently in a point in space relative to the player
    // object.
    public class CameraController : MonoBehaviour {

        public GameObject player;
        private Vector3 offset;

        // Void method called at time of ntialization
        void Start() {
            offset = transform.position - player.transform.position;
        }

        // Void method LateUpdate is used to allow for all components to be processed
        // before the camera is positioned correctly
        void LateUpdate() {
            transform.position = player.transform.position + offset;
        }
    }

___________________________________________________________________________________________________
***Player Controller Script***
___________________________________________________________________________________________________
     // Gaby Inchoco
     // Volumetric Cinema Pre-Assignment
     // 9/8/2019
     // Player Controller Script

     using System.Collections;
     using System.Collections.Generic;
     using UnityEngine;
     using UnityEngine.UI;

     // Controls aspects of the Player's Game Object like collecting items,
     // the ball's speed, and direction
     public class PlayerController : MonoBehaviour {

         // Declare public instance variables
         public float speed;
         public Text countText;
         public Text winText;
         // Declare private instance variables
         private Rigidbody rb;
         private int count;

         // Start() method which instantiates the instance variables at the opening of the game's runtime
         void Start() {
             rb = GetComponent<Rigidbody>();
             count = 0;
             SetCountText();
             winText.text = "";
             //countText.text = "Count: " + count.ToString();
         }

         // Orients the main camera to be at a fixed point in relation to the Main PLayer object 
         void FixedUpdate () {
             float moveHorizontal = Input.GetAxis("Horizontal");
             float moveVertical = Input.GetAxis("Vertical");

             Vector3 movement = new Vector3 (moveHorizontal,0.0f,moveVertical);

             rb.AddForce(movement * speed);
         }

         // OnTriggerEnter() method de-activates the pick up objects that have been collided with
         void OnTriggerEnter(Collider other) {
             if (other.gameObject.CompareTag("Pick Up")) {
                 other.gameObject.SetActive(false);    // Deactivate the gameobject
                 count = count + 1;                    // Update the counter
                 SetCountText();                       // Update the counter's text
                 }
         }
          
        // SetCountText() method updates the counter's text for each "Pick Up" object collected
        // and displays "You Win!" once all 8 items have been collected
         void SetCountText() {
             countText.text = "Count: " + count.ToString();
             if (count >= 8) {
                     winText.text = "You Win!";
                     }
               }
         }

___________________________________________________________________________________________________
***Rotate Script For Pick Up Objects***
___________________________________________________________________________________________________

    // Gaby Inchoco
    // Volumetric Cinema Pre-Assignment
    // 9/8/2019
    // Rotate Script

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;

    // This script rotates the pick up cubes so that the player can identify
    // objects to be picked up
    public class Rotate : MonoBehaviour {
        // Update is called once per frame
        void Update () {
            // We transform the object by a Vector in 3 space multiplied by the
            // change in actual time passed in Game View
            transform.Rotate(new Vector3(15,30,45) * Time.deltaTime);
        }
    }
