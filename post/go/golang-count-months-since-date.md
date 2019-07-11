---
title: "Go, count the months since a date"
date: 2017-08-28T13:53:51+02:00
tags: go
---

This simple function counts the months passed between now and a specified date:

```go
// monthsCountSince calculates the months between now
// and the createdAtTime time.Time value passed
func monthsCountSince(createdAtTime time.Time) int {
	now := time.Now()
	months := 0
	month := createdAtTime.Month()
	for createdAtTime.Before(now) {
		createdAtTime = createdAtTime.Add(time.Hour * 24)
		nextMonth := createdAtTime.Month()
		if nextMonth != month {
			months++
		}
		month = nextMonth
	}

	return months
}

//...
createdAt := time.Date(2011, 9, 2, 0, 0, 0, 0, time.UTC)
count = monthsCountSince(createdAt)
```