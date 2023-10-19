
```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
const dateFormat = "MM/DD ddd"
const filteredPages = dv.pages()
		.where(t => t.type == "log")
		.where(t => t.ActivityDate >= moment().subtract(14, "days"))
		.where(t => t.ActivityDate <= moment().subtract(7, "days"))
		.sort(p=>p.ActivityDate, "desc")
const countWorkouts = filteredPages.length

dv.header(3, `Prior 7 Days, ${countWorkouts} workouts`)
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
```
