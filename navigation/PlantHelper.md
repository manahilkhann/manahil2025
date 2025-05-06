---
layout: page
title: Plant
permalink: /PlantHelper/
---

<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f2f2f2;
        margin: 0;
        padding: 0;
        height: 50vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 80px;
    }
    .container {
        background-color: #ffffff;
        border-radius: 8px;
        padding: 30px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        width: 350px;
        text-align: center;
    }
    h3 {
        color: rgb(35, 77, 37);
        font-size: 24px;
    }
    label {
        font-size: 16px;
        margin-bottom: 10px;
        display: block;
    }
    input {
        padding: 10px;
        width: 100%;
        margin: 10px 0 20px 0;
        border: 2px solid #ddd;
        border-radius: 4px;
        font-size: 16px;
    }
    button {
        padding: 10px 20px;
        background-color:rgb(82, 128, 85);
        color: white;
        border: none;
        border-radius: 4px;
        font-size: 16px;
        cursor: pointer;
        transition: background-color 0.3s;
    }
    button:hover {
        background-color:rgb(64, 100, 66);
    }
    .result {
        padding: 10px;
        border-radius: 4px;
        margin-top: 10px;
    }
    .water-info {
        background-color: #d4edda;
        color: #28a745;
    }
    .water-needed {
        background-color: #ffcccb;
        color: #d9534f;
    }
    .water-not-needed {
        background-color: #d4edda;
        color: #28a745;
    }
    .error {
        background-color: #f8d7da;
        color: #721c24;
    }
</style>

<div class="wrapper">
    <!-- Plant Watering Guide -->
    <div class="container">
        <h1>🌱 Plant Watering Guide 🌱</h1>
        <label for="userPlant">What type of plant do you have?</label>
        <input type="text" id="userPlant" placeholder="e.g., Cactus">
        <button onclick="getWateringInfo()">Get Watering Info</button>
        <div id="response"></div>
    </div>
    <!-- Plant Watering Reminder -->
    <div class="container">
        <h1>🌱 Plant Watering Reminder 🌱</h1>
        <label for="plantType">Plant Type:</label>
        <input type="text" id="plantType" placeholder="e.g., Cactus">
        <label for="lastWatered">Last Watered (MM-DD-YYYY):</label>
        <input type="date" id="lastWatered">
        <button onclick="checkWatering()">Check Watering Status</button>
        <div id="output"></div>
    </div>
</div>

<script>
    function getWateringInfo() {
        const userPlant = document.getElementById("userPlant").value.toLowerCase();
        const response = document.getElementById("response");
        let wateringInfo = "";
        response.className = "result"; // Clear previous classes
        if (userPlant === "cactus") {
            wateringInfo = "Cacti need very little water. Water them once every 2-3 weeks.";
            response.classList.add("water-info");
        } else if (userPlant === "fern") {
            wateringInfo = "Ferns like to be kept moist. Water them once a week.";
            response.classList.add("water-info");
        } else if (userPlant === "bamboo") {
            wateringInfo = "Bamboo needs a lot of water. Water them every 2-3 days.";
            response.classList.add("water-info");
        } else if (userPlant === "succulent") {
            wateringInfo = "Succulents need moderate water. Water them every 1-2 weeks.";
            response.classList.add("water-info");
        } else if (userPlant === "orchid") {
            wateringInfo = "Orchids like to dry out between waterings. Water them every 1-2 weeks.";
            response.classList.add("water-info");
        } else {
            wateringInfo = "❌ Sorry, I don't have information on that type of plant.";
            response.classList.add("error");
        }
        response.innerHTML = wateringInfo;
    }
    function checkWatering() {
        const plants = [
            { name: "Cactus", interval: 10 },
            { name: "Fern", interval: 3 },
            { name: "Orchid", interval: 7 },
            { name: "Bamboo", interval: 2 },
            { name: "Succulent", interval: 14 }
        ];
        const plantType = document.getElementById("plantType").value.trim();
        const lastWatered = document.getElementById("lastWatered").value;
        const output = document.getElementById("output");
        output.className = "result"; // Clear previous classes
        if (!plantType || !lastWatered) {
            output.classList.add("error");
            output.innerHTML = "❌ Please enter both the plant type and the last watered date.";
            return;
        }
        const today = new Date();
        const lastDate = new Date(lastWatered);
        if (isNaN(lastDate)) {
            output.classList.add("error");
            output.innerHTML = "❌ Invalid date. Please enter a valid date.";
            return;
        }
        const daysSinceWatered = Math.floor((today - lastDate) / (1000 * 60 * 60 * 24));
        let found = false;
        for (let plant of plants) {
            if (plant.name.toLowerCase() === plantType.toLowerCase()) {
                found = true;
                if (daysSinceWatered >= plant.interval) {
                    output.classList.add("water needed");
                    output.innerHTML = `🌱 Your ${plant.name} needs watering! (${daysSinceWatered} days since last watered)`;
                } else {
                    output.classList.add("water not needed");
                    output.innerHTML = `✅ Your ${plant.name} is fine. Only ${daysSinceWatered} days since last watered.`;
                }
                break;
            }
        }
        if (!found) {
            output.classList.add("error");
            output.innerHTML = "❌ Sorry, that plant is not in our database.";
        }
    }
</script>


