---
layout: base
title: Cookie Clicker
permalink: /games/cc
---

{% include nav/games.html %}

<div id="cookie-clicker" style="text-align: center; margin: auto; width: 400px;">
    <h1>Cookie Clicker</h1>
    <button id="cookieButton" style="font-size: 24px; padding: 20px;">🍪 Click Me!</button>
    <div id="score" style="margin-top: 20px; font-size: 20px; color: white;">Cookies: 0</div>
    <div id="multiplier" style="margin-top: 10px; font-size: 20px; color: white;">Click Multiplier: 1</div>
    <button id="upgradeButton" style="margin-top: 20px; font-size: 20px; padding: 10px;">Upgrade Multiplier (Cost: 10 cookies)</button>
</div>

<script>
    let cookies = 0;
    let multiplier = 1;

    const cookieButton = document.getElementById("cookieButton");
    const scoreDisplay = document.getElementById("score");
    const multiplierDisplay = document.getElementById("multiplier");
    const upgradeButton = document.getElementById("upgradeButton");

    cookieButton.addEventListener("click", () => {
        cookies += multiplier;
        updateDisplay();
    });

    upgradeButton.addEventListener("click", () => {
        const upgradeCost = Math.floor(10 * Math.pow(1.5, multiplier - 1)); // Increasing cost
        if (cookies >= upgradeCost) {
            cookies -= upgradeCost;
            multiplier++;
            updateDisplay();
        } else {
            alert("Not enough cookies!");
        }
    });

    function updateDisplay() {
        scoreDisplay.innerText = "Cookies: " + cookies;
        multiplierDisplay.innerText = "Click Multiplier: " + multiplier;
        upgradeButton.innerText = "Upgrade Multiplier (Cost: " + Math.floor(10 * Math.pow(1.5, multiplier - 1)) + " cookies)";
    }
</script>
