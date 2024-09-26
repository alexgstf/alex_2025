---
layout: post
title: About
permalink: /about/
comments: true
---

<style>
    #codeimg {
        display: block;
        margin-left: 30px;
        float: right;
    }
</style>

---

#### Some Facts About Me

<br>

- I am the second youngest in a family of 5
- I play the trombone in marching, concert, and jazz band at DNHS
- My best subject in school is math

<br>

<img id="codeimg" src="https://imageio.forbes.com/blogs-images/forbestechcouncil/files/2019/01/canva-photo-editor-8-7.png" width="300" height="300">

My name is Alex Gustaf and I'm currently a senior at Del Norte High School! I joined CSP because I am interested in working with computers and creating cool projects from my own code. Also, I've already learned a little about languages like Python and HTML, so I knew that I wanted to continue developing my skills.

#### Background

I have lived here in San Diego, CA my whole life with my family. I went to Stone Ranch and Oak Valley before attending Del Norte. My dad grew up in Michigan but moved here, where he met my mom who had immigrated from China. 

<br>

<style>
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(125px, 1fr));
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px;
        object-fit: contain;
    }
    .grid-item p {
        margin: 5px 0;
    }
</style>

<div class="grid-container" id="grid_container"> </div>

<script>
    var container = document.getElementById("grid_container");

    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "0/01/Flag_of_California.svg", "description": "California"},
        {"flag": "b/b5/Flag_of_Michigan.svg", "description": "Michigan"},
        {"flag": "a/a4/Flag_of_the_United_States.svg", "description": "USA"},
        {"flag": "f/fa/Flag_of_the_People%27s_Republic_of_China.svg", "description": "China"},
    ]; 

    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";
        var img = document.createElement("img");
        img.src = http_source + location.flag; 
        img.alt = location.flag + " Flag"; 

        var description = document.createElement("p");
        description.textContent = location.description;

        gridItem.appendChild(img);
        gridItem.appendChild(description);

        container.appendChild(gridItem);
    }
</script>

