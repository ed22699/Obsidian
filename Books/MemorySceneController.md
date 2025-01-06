---
tags:
  - Unity
  - Script
---
- The logic for a memory game.
	- creates a grid of spaced cards
	- compares flipped cards
	- can reset game
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
// Include TextMeshPro code
using TMPro;
using UnityEngine.SceneManagement;

public class SceneController : MonoBehaviour
{
    private MemoryCard firstRevealed;
    private MemoryCard secondRevealed;
    private int score = 0;
    
    // Spacing the grid
    public const int gridRows = 2;
    public const int gridCols = 4;
    public const float offsetX = 2f;
    public const float offsetY = 2.5f;
    [SerializeField] MemoryCard originalCard;
    [SerializeField] Sprite[] images;
    [SerializeField] TMP_Text scoreLabel;

    public bool canReveal
    {
        // Getter function that returns false if a second card is already revealed
        get { return secondRevealed == null; }
    }

    public void CardRevealed(MemoryCard card)
    {
        if (firstRevealed == null)
        {
            firstRevealed = card;
        }
        else
        {
            secondRevealed = card;
            StartCoroutine(CheckMatch());
        }
    }
    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // Position of the first card (all other cards willll be offset from here)
        Vector3 startPos = originalCard.transform.position;

        // declare an integer array with a pair of IDs
        int[] numbers = { 0, 0, 1, 1, 2, 2, 3, 3 };
        numbers = ShuffleArray(numbers);
        
        for (int i = 0; i < gridCols; i++)
        {
            for (int j = 0; j < gridRows; j++)
            {
                // Container reference for either the original card or the copies
                MemoryCard card;
                if (i == 0 && j == 0)
                {
                    card = originalCard;
                } else
                {
                    card = Instantiate(originalCard) as MemoryCard;
                }

                int index = j * gridCols + i;
                int id = numbers[index];
                // Call the public method we added to MemoryCard
                card.SetCard(id, images[id]);

                float posX = (offsetX * i) + startPos.x;
                float posY = -(offsetY * j) + startPos.y;
                card.transform.position = new Vector3(posX, posY, startPos.z);
            }
        }
    }

    // Implementation of the Knuth shuffle algorithm
    private int[] ShuffleArray(int[] numbers)
    {
        int[] newArray = numbers.Clone() as int[];
        for (int i = 0; i < newArray.Length; i++)
        {
            int tmp = newArray[i];
            int r = Random.Range(i, newArray.Length);
            newArray[i] = newArray[r];
            newArray[r] = tmp;
        }

        return newArray;
    }

    private IEnumerator CheckMatch()
    {
        if (firstRevealed.Id == secondRevealed.Id)
        {
            score++;
            scoreLabel.text = $"Score: {score}";
        }
        else
        {
            yield return new WaitForSeconds(.5f);

            // Unreveal cards if they do not match
            firstRevealed.Unreveal();
            secondRevealed.Unreveal();
        }

        // Clear out the variables
        firstRevealed = null;
        secondRevealed = null;
    }

    public void Restart()
    {
        // If your scene has a different name change the namge in this string
        SceneManager.LoadScene("SampleScene");
    }

}
```