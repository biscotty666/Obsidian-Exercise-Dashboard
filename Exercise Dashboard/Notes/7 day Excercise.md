
```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
const filteredPages = dv.pages()
		.where(b => b.type == "log")
		.where(b => b.ActivityDate >= moment().subtract(7, "days"))
	 	.sort(p => p.ActivityDate, "desc")
const countWorkouts = filteredPages.length
const dateFormat = "MM/DD ddd"
dv.header(3, `7 Days, ${countWorkouts} Workouts`)
dv.table(["🗓️","🚶/🚴", "📓", "⏱️", "🗺️"],
	await Promise.all(filteredPages
		.map(async b=>[
			moment(new Date(b.ActivityDate)).format(dateFormat),
			await f(dv, b, "Activity"), 
			await f(dv, b, "Distance"), 
			await f(dv, b, "Duration"), 
			await f(dv, b, "Route"),
		]
	)
	)
)
dv.container.className += " db-exercise"
```


