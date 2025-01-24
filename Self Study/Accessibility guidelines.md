- approximately one in seven people have a disability that affects the way they interact with the world and their devices
- prioritising *simplicity* and *perceivability* and examining every design decision to ensure that it doesn't  exclude people with disabilities or who interact with their devices in different ways
	- simplicity - support familiar, consistent interactions that make complex tasks simple and straightforward to perform
	- perceivability - make sure that all content can be perceived whether people are using sight, hearing, or tough
- support personalisation
	- Bold text, larger text, invert colours, increase contrast options
- consider using Xcode's *Accessibility Inspector*
- VoiceOver, Assistive Touch, Pointer Control, and Switch Control need to be supported correctly
## Gestures
- *don't override platform gestures*, swiping down should reveal Notification centre regardless of the app
- prefer *simplified gestures* for *common interactions*. Complex gestures such as multifinger or multihand, long presses or gestures that require repeated movements are challenging
- *provide alternative ways to perform gesture-based actions*. Include an option for people who may not be able to perform a specific gesture. e.g. if people can use a gesture to delete a row provide a way to delete items through an edit mode or by offering a Delete button in an item detail view
- when possible app's *core functionality* should be accessible through *more than one type of physical interaction*
	- camera can take photo with button or device's volume button
- *custom gestures* should *support assistive technologies* that give people alternative ways to interact with your app. See `UIAccessibilityCustomAction`
- Make drag and drop accessible in app. `accessibilityDragSourceDescriptors` and `accessibilityDropPointDescriptors`
## Buttons and controls
- Give all controls and interactive elements a *hit target that's large enough*. At least 44x44pt in visionOS
	- Centres of controls should be at least 60pt apart
- *Characterise the accessibility of custom elements*. `button` or `NSAccessibilityButton` can be used to characterise a view as a button means VoiceOver speaks the view's description followed by the word button
- Use *consistent style hierarchy* to communicate the *relative importance* of buttons. Visually prominent filled style for the button that perform the most likely action, grey or plain for buttons with less important actions. See `UIButton.Configuratoin`
- *Prefer the system-provided switch component*, e.g. on off switch system-provided icon has a I and O to indicate on or off
- Consider giving links a visual indicator in addition to colour, such as an underline
## User input
- Let people input information by *speaking* instead of typing or gesturing (add a dictation button to a text entry field)
- *Support Siri* or Shortcuts for performing *important tasks* by voice alone
- When possible, *don't prevent people from selecting plain text*. Many people rely on using selected text as input for translations and definitions
## Haptics
- Support the system-defined haptics where available
## Content descriptions
- Provide *alternative descriptions for all images* that convey meaning
- Make infographics fully accessible, provide concise description
- When an image is purely *decorative* and isn't intended to communicate anything important *hide* it from assistive technologies
- Give each page a *unique title* and provide headings that identify sections in your information hierarchy
- provide closed captions, audio descriptions and transcripts for video and audio
## Navigation
- Make sure *VoiceOver users can navigate to every element*
- Improve the VoiceOver experience by *specifying* how elements are *grouped*, ordered or linked (`shouldGroupAccessibilityChildren` and `accessibilityTitleUIElement()`)
- Tell VoiceOver when visible content or layout changes (`UIAccessibility.Notification` or `NSAccessibility.Notification`)
- Help people predict when a control opens a different webpage or app
- Provide alternative text labels for all important interface elements
- Support the VoiceOver rotor when necessary (navigates a document or webpage by headings, links or other section types, can also bring up the braille keyboard `UIAccessibilityCustomRotor` and `NSAccessibilityCustomRotor`)
## Text display
- *use Dynamic type* and test that your app's layout adapts to all font sizes
- As font size increases, keep *text truncation* to a *minimum*. Aim to display as much useful text in the largest accessibility font size as you do in the largest standard font size
- Consider adjusting layout at large font sizes
- Increase the *size* of meaningful interface *icons* as font size increases
- Maintain a *consistent information hierarchy* regardless of the current font size
- Prefer *regular or heavy font weights* in your app (avoid Ultralight, Thin and Light font weights)
- Ensure your app *responds* correctly and looks good when people turn on *bold text*
- Make sure custom *fonts are legible*, usually best to use the system fonts
- Avoid full text justification
- Avoid italics or all caps for long passages of text
## Colour and effects
- *Don't rely solely on colour* to differentiate between objects or communicate important information. If colour used to convey information be sure to provide text labels or glyph shapes to help everyone perceive it
- Prefer *system colours for text* (responds correctly to settings such as invert colours or increase contrast)
- *Avoid using colour combinations* as the only way to *distinguish* between two states or values
- Ensure views respond correctly to *invert colours*
- Use *strongly contrasting colours* to improve *readability*
	- can use Xcode's Accessibility Inspector or an online colour calculator based on the Web Content Accessibility Guidelines

| Text size            | Text weight | Minimum contrast ratio |
|:-------------------- | ----------- | ---------------------- |
| Up to 17 points      | All         | 4.5:1                  |
| 18 points and larger | All         | 3:1                    |
| All                  | Bold        | 3:1                    |
- Change blurring and transparency when people turn on Reduce Transparency
## Motion
- *Avoid requiring animations* unless they're essential for your experience
- *Play tightened animations when Reduce Motion is on*
	- tighten springs to reduce bounce effects or track 1:1 as a person gestures
	- Avoid animating depth changes in z-axis layers
	- Avoid animating into or out of blurs
	- Replace a slide with a fade to avoid motion
- Let people control video and other motion effects (*avoid autoplaying*)
- Be cautious when displaying moving or blinking elements
