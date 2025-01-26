## Adaptability
- need to handle:
	- different screen sizes, resolutions and colour spaces
	- different orientations
	- system features like dynamic island and camera controls
	- dynamic type text-size changes
	- locale-based internationalisation features like left-to-right/right-to-left layout direction, date/time/number formatting, font variation and text length
- design a layout that adapts gracefully to context changes while remaining recognisably consistent
- be prepared for text-size changes
- preview your app on multiple devices, using different orientations, localisations, and text sizes
- when necessary, scale artwork in response to display changes
## Visual hierarchy
- Use placement to convey relative importance. Place the most important item in the top leading side of the window
- Make essential information easy to find by giving it sufficient space
- Create visual groupings to help people find the information they want. Use negative space, background shapes, colours, materials, or separator lines to show when elements are related
- Use alignment to ease visual scanning and to communicate organisation and hierarchy
- Consider providing visual hints to help people discover content that's currently hidden
- Make interactive components easy to discover by providing enough space around them
## Guides and safe areas
- they system include predefined layout guiders. See `UILayoutGuide` and `NSLayoutGuide`
- safe area is area within a view that isn't covered by a navigation bar, tab bar, toolbar, or other views a window might provide.
- Respect key display and system features in each platform
## iOS
- Aim to support both portrait and landscape orientations
- Extend visual content to fill the screen
- Inset full-width buttons. A full-width button at the bottom of the screen generally looks best when it has rounded corners and it aligns with the bottom of the safe area
- Avoid placing interactive controls at the bottom edge of the screen when possible. Also avoid placing controls in the far corners of the screen because there areas can be difficult for people to reach comfortably
- Be prepared for different status bar heights
- Hide the status bar only when it adds vaue or enhances your experience