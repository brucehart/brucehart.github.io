---
author: brucehart
comments: true
date: 2024-10-30 17:36:00+00:00
layout: post
link: https://www.bhart.org/Sample-Post
slug: sample-post
title: 'Sample Post'
---

# Sample post

This is some sample text to go along with my post.

```javascript
var teams = [];
var table = document.querySelector('.matchups-body table tbody');

if (!table) {
    console.error("Table not found within .matchups-body. Please check the structure.");
} else {
    var tableRows = table.querySelectorAll('tr');

    tableRows.forEach(function(row) {
        var teamNameWithStanding = row.querySelector('td:nth-child(3)').textContent.trim();
        var projectedPoints = parseFloat(row.querySelector('td:nth-child(4)').textContent.trim());

        // Remove the standing position at the end (e.g., "1st", "2nd", "3rd", etc.)
        // Assuming standings are always the last word and look like "1st", "2nd", "3rd", etc.
        var teamNameParts = teamNameWithStanding.split(' ');
        var lastPart = teamNameParts[teamNameParts.length - 1];

        // Check if the last part is a standing (contains 'st', 'nd', 'rd', or 'th')
        if (/\d+(st|nd|rd|th)$/.test(lastPart)) {
            teamNameParts.pop(); // Remove the last part if it's a standing
        }

        var cleanTeamName = teamNameParts.join(' '); // Rejoin the remaining parts as the team name

        // Only include teams with points greater than 0
        if (projectedPoints > 0) {
            teams.push([cleanTeamName, projectedPoints]);
        }
    });

    // Format the data as a string that can be copied
    var formattedData = teams.map(function(team) {
        return `${team[0]}, ${team[1]}`;
    }).join('\n');

    // Copy the formatted data to the clipboard
    copy(formattedData);

    console.log("Data copied to clipboard:\n", formattedData);
}
```


