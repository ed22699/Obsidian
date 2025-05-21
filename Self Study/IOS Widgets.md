---
tags:
  - swift
---
- three sizes small, medium and large
- not mini apps, glanceable information
- build with WidgetKit
- you build an upfront timeline, e.g. update every 2 hours
	- has an update budget
	- unless *live action*
- add *Widget Extension* to your app
## TimelineProvider
- a type that defines when to update the widgets display
- three functions:
	- placeholder: what the widget will look like when there is no data
	- getSnapshot: what the widget looks like right now
	- getTimeline: where the timeline actually gets created
		- has entries - the data (e.g. the time) an array of type TimelineEntry (always needs a date)
		- with the entries you do the following:
			```swift
			let timeline = Timeline(entries: entries, policy: .atEnd)
			completion(timeline)
			```
		- can do `.atEnd`, `.never`, `.after`
- TimelineEntry is what you populate the data with (needs a date), consider this your DataModel
- You will have a view that takes in an entry and create the view
- You will have a Widget: this is the actual widget: two types of configuration:
	- static configuration: like a static view
	- Intent configuration: can hold onto your widget and customise it in some way