---
layout: page
title: About
permalink: /about/
---

### Introduction

Hello, my name is Alex Gustaf and I'm currently a senior at Del Norte High School! I joined CSP because I am interested in working with computers and creating cool projects from my own code. Also, I've already learned a little about languages like Python and HTML, so I knew that I wanted to continue developing my skills.

<img src="https://images.unsplash.com/photo-1515879218367-8466d910aaa4?fm=jpg&q=60&w=3000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8Y29kaW5nfGVufDB8fDB8fHww" width="400" height="300">

### About me

I have lived here in San Diego, CA my whole life with my parents, older sister and younger brother. I went to Stone Ranch and Oak Valley before attending Del Norte. My dad grew up in Michigan but moved here, where he met my mom who had immigrated from China. 

<style>
    /* Style looks pretty compact, trace grid-container and grid-item in the code */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }
</style>

<!-- This grid_container class is for the CSS styling, the id is for JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "0/01/Flag_of_California.svg", "description": "California"},
        {"flag": "b/b5/Flag_of_Michigan.svg", "description": "Michigan"},
        {"flag": "a/a4/Flag_of_the_United_States.svg", "description": "USA"},
        {"flag": "f/fa/Flag_of_the_People%27s_Republic_of_China.svg", "description": "China"},
    ]; 
    
    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = location.description; // extract the description

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>