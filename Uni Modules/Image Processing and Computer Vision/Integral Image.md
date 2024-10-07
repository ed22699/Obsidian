---
tags:
  - viola_jones_detector
---

- calculating features on top of regions to make it less costly
- solution is to create an image of the same size where the pixels are the sum of the pixels before it (starting at 0,0 in the image)
![[Screenshot 2024-10-07 at 15.32.24.png|300]]
![[Screenshot 2024-10-07 at 15.34.24.png|100]]
- to calculate the sum of the pixels in a square take the top right of that square and subtract the relevant side squares (green and red) then add back the overlap thats been removed twice (blue)
![[Screenshot 2024-10-07 at 15.37.53.png|500]]