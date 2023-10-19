```dataviewjs
/* Create sets of pages */

const currentPages = dv.pages() 
								.where(b => b.type == "log")
								.where(b => b.ActivityDate >= moment().subtract(30, "days"))
const priorPages = dv.pages() 
								.where(b => b.type == "log")
								.where(b => b.ActivityDate >= moment().subtract(60, "days"))
								.where(b => b.ActivityDate <= moment().subtract(30, "days")) 
const currentWalkPages = currentPages
								.where(b => b.Activity == "🚶")
const currentBikePages = currentPages
								.where(b => b.Activity == "🚴")
const priorWalkPages = priorPages
								.where(b => b.Activity == "🚶")
const priorBikePages = priorPages
								.where(b => b.Activity == "🚴")

/* Function to sum the distances, duration */

function sumStat (stat, thePages) {
	const pageValues = thePages.values
	if (stat == "duration") {
		return pageValues
		  .reduce((sum, b) => sum + b.Duration, 0)
	}
	
	if (stat == "distance") {
		return pageValues
		  .reduce((sum, b) => sum + b.Distance, 0)
	}
}

/* Function to convert minutes to hours */

function toHours (time) {
 return (time / 60).toFixed(1)
}

/* Calculate the distances (6 values) */

const totalCurrentDistance = sumStat("distance",currentPages).toFixed(1)
const totalCurrentWalkDistance = sumStat("distance",currentWalkPages).toFixed(1)
const totalCurrentBikeDistance = sumStat("distance",currentBikePages).toFixed(1)
const totalPriorDistance = sumStat("distance",priorPages).toFixed(1)
const totalPriorWalkDistance = sumStat("distance",priorWalkPages).toFixed(1)
const totalPriorBikeDistance = sumStat("distance",priorBikePages).toFixed(1)

/* Calculate the durations (6 values) */

const totalCurrentTime = toHours(sumStat("duration",currentPages))
const totalCurrentWalkTime = toHours(sumStat("duration",currentWalkPages))
const totalCurrentBikeTime = toHours(sumStat("duration",currentBikePages))
const totalPriorTime = toHours(sumStat("duration",priorPages))
const totalPriorWalkTime = toHours(sumStat("duration",priorWalkPages))
const totalPriorBikeTime = toHours(sumStat("duration",priorBikePages))

/* Calculate the speed (4 values) */

const currentWalkSpeed = (totalCurrentWalkDistance / totalCurrentWalkTime).toFixed(1)
const priorWalkSpeed = (totalPriorWalkDistance / totalPriorWalkTime).toFixed(1)
const currentBikeSpeed = (totalCurrentBikeDistance / totalCurrentBikeTime).toFixed(1)
const priorBikeSpeed = (totalPriorBikeDistance / totalPriorBikeTime).toFixed(1)

/* Count the workouts */

const currentCount = currentPages.length
const priorCount = priorPages.length
const currentBikeCount = currentBikePages.length
const priorBikeCount = priorBikePages.length
const currentWalkCount = currentWalkPages.length
const priorWalkCount = priorWalkPages.length



/* Create an array (list) and add the table rows
   The first table displays the distance and duration */
   
let rowsT1 = []
rowsT1.push(["Miles", totalCurrentDistance, totalPriorDistance])
rowsT1.push(["🚶", totalCurrentWalkDistance, totalPriorWalkDistance])
rowsT1.push(["🚴", totalCurrentBikeDistance, totalPriorBikeDistance])
rowsT1.push(["","",""])
rowsT1.push(["Hours", totalCurrentTime, totalPriorTime])
rowsT1.push(["🚶", totalCurrentWalkTime, totalPriorWalkTime])
rowsT1.push(["🚴", totalCurrentBikeTime, totalPriorBikeTime])
rowsT1.push(["","",""])
rowsT1.push(["Speed (m/h)", "", ""])
rowsT1.push(["🚶", currentWalkSpeed, priorWalkSpeed])
rowsT1.push(["🚴", currentBikeSpeed, priorBikeSpeed])
rowsT1.push(["","",""])
rowsT1.push(["Workouts", currentCount, priorCount])
rowsT1.push(["🚶", currentWalkCount, priorWalkCount])
rowsT1.push(["🚴", currentBikeCount, priorBikeCount])

/* Create the table header */

const tableHeader = ["","Current","Prior"]

/* Display the table */

dv.header(3, "30 Day Stats")
dv.table(tableHeader, rowsT1)
```
