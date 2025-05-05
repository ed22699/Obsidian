---
tags:
  - swift
---
## Documentation Window
- two main types
	- primary documentation: for cocoa classes and other symbols is included entirely within Xcode, is displayed in the documentation window ($Window \rightarrow Developer \; Documentation \; or \; Help \rightarrow Developer \; Documentation$) 
	- secondary documentation: older guides, sample code, and technical notes and Q&As available only online
## Quick help
- you can inject documentation for your own code into Quick Help. Precede a declaration with a comment enclosed in `/** */` or with one ore more single line comments starting with `///`
- markdown formatting can be used
- the first line of the comment becomes the summary field for Quick Help; remaining paragraphs become the Description field, except that certain list items 
	- paragraphs beginning with `*` or `-` followed by space are treated in a special way such as
		- list items beginning with `Parameter paramname:` are incorporated into the parameters field
		- a list item beginning with `Throws:` becomes the Throws field
		- a list item beginning with `Returns:` becomes the returns field
		- a list item beginning with `Note:` becomes a note field