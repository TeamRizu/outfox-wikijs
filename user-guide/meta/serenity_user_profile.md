---
title: Serenity User Profile
description: 
published: true
date: 2023-06-20T21:21:53.173Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:24:01.113Z
---

<div style="display: flex; align-items: center; flex-direction: column;">
  <label for="user-select">Select User:</label>

  <select name="users" id="user-select" style="min-width: 260px; width: 30%; padding: 16px 20px; border-color: #019b81; border: solid; border-width: 2px; border-radius: 8px; background-color: #003028;">
    <option value="">Select an option</option>
  </select>
</div>

---

<div style="display: flex; flex-direction: column; align-items: center;">

  <h1 id="userName"></h1>

  <div id= 'profileContent'>
    <div id="tagsDiv" style="display: none;">
      <h2 style="align-self: center;">Tags</h2>
      <div id='tagsRow' style="display: flex; flex-wrap: wrap; justify-items: center; justify-content: center; gap: 30px;">
      </div>
      <h2 style="align-self: center;">Resume</h2>
      <p style="align-self: center;" id="userResume">Select user to view resume.</p>  
      <!-- Daniel Rotwind has submitted 93 charts, 4 songs and 9 graphics for Project OutFox Serenity.-->
      <p style="align-self: center;" id="userMostChartsForSong">Most Charted Song: Select User to View.</p>
      <p style="align-self: center;" id="userMostChartsForMode">Most Charted Mode: Select User to View</p>
    </div>
    <div id="socialsOuterDiv" style="display: none;">
      <h2 style="align-self: center;">User Socials</h2>
        <div id='socials' style="display: flex; flex-wrap: wrap; justify-items: center; justify-content: center; gap: 30px;">
        </div>
    </div>
    <div style="overflow-x:auto; display: none;" id="userSongSubmissionDiv">
      <h2 style="align-self: center;">Song Submissions</h2>
    </div>
    <div style="overflow-x:auto; display: none;" id="userGraphicSubmissionDiv">
      <h2 style="align-self: center;">Graphic Submissions</h2>
    </div>
    <div style="overflow-x:auto; display: none;" id="userChartSubmissionDiv">
      <h2 style="align-self: center;">Chart Submission</h2>
    </div>
    <br>
    If you want a social add/removed from your profile then join the <a href="https://discord.gg/cN4TjgQdcA">Project OutFox Discord Server</a> and contact the moderator team.
    <div id="copyData" style="display: none;">
      <br>
      Want the data that we have stored for this profile? Click the button bellow and the JSON Object will be copied to your clipboard. (Tags not included!)
      <br>
      <span class="letter-button" style="width: 226px; align-self: center;">
        <a class="letter-button-text" style="cursor: pointer;">
          Copy Data to Clipboard
        </a>
      </span>
    </div>
  </div>
</div>

_Written and Maintained by Moru Zerinho6_