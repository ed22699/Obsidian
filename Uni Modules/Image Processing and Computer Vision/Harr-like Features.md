---
tags:
  - viola_jones_detector
---
- feature = sum of white pixels - sum of black pixels
![[Screenshot 2024-10-07 at 15.14.52.png|200]]
![[Screenshot 2024-10-07 at 15.16.23.png|80]]
- if hard edge the filter will produce a large number (below with filter 1 produces 2040)
 ![[Screenshot 2024-10-07 at 15.17.08.png|80]]
- soft edge will produce a smaller number (below with filter 1 produces 1245)
![[Screenshot 2024-10-07 at 15.18.24.png|80]]
- no edge will produce a very small number (below with filter 1 produces 17)
![[Screenshot 2024-10-07 at 15.18.48.png|80]]
![[Drawing 2024-10-07 15.20.12.excalidraw|400]]
>[!note]
diagonal features are less commonly used as they can sometimes result in more processing with an integral image