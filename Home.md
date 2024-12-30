---
cssclasses:
  - dashboard
banner: "![[home.jpg]]"
banner_y: 0
---

<div class="title" style="color:white">HOME</div>

# Trackers
- 👨‍💻 Code
	- ```tracker
	searchType: frontmatter, frontmatter
	searchTarget: date, HoursCoded
	xDataset: 0
	fixedScale: 0.7
	folder: Journal/Weekly Notes
	line:
		fillGap: true
		title: Personal Project Weekly Coding Hours
		yAxisLabel: Hours
		yMin: 0
		yAxisTickInterval: 1
		xAxisTickInterval: 1w


	- ```tracker
	searchType: frontmatter, frontmatter
	searchTarget: date, HoursCoded
	xDataset: 0
	folder: Journal/Weekly Notes
	summary:
		template: "Maximum: {{max()}} hours\nAverage: {{average()}} hours"
- 📚 Reading
	- ```tracker
	searchType: frontmatter
	searchTarget: PagesRead
	folder: Journal/Daily Notes
	datasetName: Reading
	fixedScale: 0.7
	month:
	- ```tracker
	searchType: frontmatter
	searchTarget: PagesRead
	folder: Journal/Daily Notes
	summary:
	    template: "Longest Streak: {{maxStreak()}} day(s)\nLongest Breaks: {{maxBreaks()}} day(s)\nLast streak: {{currentStreak()}} day(s)\nTotal Pages: {{sum()}}"
# Uni
- 🗄️ Recent file updates
 `$=dv.list(dv.pages('"Uni Modules"').sort(f=>f.file.mtime.ts,"desc").limit(5).file.link)`
- 📚 Modules
	- [[Uni Modules/Machine Learning/Index|Machine Learning]]
	- [[Uni Modules/Image Processing and Computer Vision/Index|Image Processing and Computer Vision]]
	- [[Uni Modules/Design Verification/Index|Design Verification]]
	- [[Uni Modules/Advanced Algorithms/Index|Advanced Algorithms]]

 # Personal
 - ✍️ Goals
	 - [[Coding]]
	 - [[Reading]]
	 - [[Van Build]]
	 - [[Startup]]
- 📚 Reading
	- [[Books]]

# Work
- ❓ Leet Code
	- [[Problems]]

# Vault Info
- 🗄️ Recent file updates
 `$=dv.list(dv.pages('').sort(f=>f.file.mtime.ts,"desc").limit(5).file.link)`
- 🔖 Tagged:  favorite 
 `$=dv.list(dv.pages('#favorite').sort(f=>f.file.name,"desc").limit(4).file.link)`
- 〽️ Stats
	-  File Count: `$=dv.pages().length`