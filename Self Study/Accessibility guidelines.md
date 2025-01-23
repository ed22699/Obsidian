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