- System-provided UI frameworks support right-to-left by default
## Text alignment
- Adjust text alignment to match the interface direction, if the system doesn't do so automatically
- Align a paragraph based on its language, not on the current context
- Use a consistent alignment for all text items in a list
## Numbers and characters
- Don't reverse the order of numerals in a specific number
- Reverse the order of numerals that show progress or a counting direction; never flip the numerals themselves
## Controls
- Flip controls that show progress from one value to another
- Flip controls that help people navigate or access items in a fixed order
- Preserve the direction of a control that refers to an actual direction or points to an onscreen area. E.g. if you provide a control that means "to the right", it must always point right, regardless of the current context
- Visually balance adjacent Latin and RTL scripts when necessary. In buttons, labels, and titles, Arabic or Hebrew can appear too small when next to uppercased Latin text as they don't include uppercase letters. It often works well to increase the RTL font size by about 2 points
## Images
- Avoid flipping images like photographs, illustrations, and general artwork
- Reverse the positions of images where their order is meaningful
## Interface icons
- Flip interface icons that represent text or reading direction
- Consider creating a localised version of an interface icon that displays text
- Flip an interface icon that shows forward or backward motion
- Don't flip logos or universal signs and marks
- In general, avoid flipping interface icons that depict real-world objects
- Before merely flipping a complex custom interface icon, consider its individual components and the overall visual balance
