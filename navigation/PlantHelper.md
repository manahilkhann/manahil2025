---
layout: page
title: Plant
permalink: /PlantHelper/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
<div class="wrapper">
    <div class="container">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #ffffff;
            border-radius: 8px;
            padding: 30px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            width: 350px;
            text-align: center;
        }
        h1 {
            color: #4CAF50;
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
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        #response {
            font-size: 18px;
            font-weight: bold;
            margin-top: 20px;
        }
        .result {
            padding: 10px;
            border-radius: 4px;
            margin-top: 10px;
        }
        .water-info {
            background-color: #d4edda; /* Light green */
            color: #28a745; /* Green text */
        }
        .error {
            background-color: #f8d7da;
            color: #721c24;
        }
    </style>
    </div>
    <div class="container">
        <h1>🌱 Plant Watering Guide 🌱</h1>
        <label for="userPlant">What type of plant do you have?</label>
        <input type="text" id="userPlant" placeholder="e.g., cactus"><br>
        <button onclick="getWateringInfo()">Get Watering Info</button>
        <div id="response"></div>
    </div>
    <script>
        function getWateringInfo() {
            const userPlant = document.getElementById("userPlant").value.toLowerCase();
            const response = document.getElementById("response");
            let wateringInfo = "";
            // Plant watering info based on user input
            if (userPlant === "cactus") {
                wateringInfo = "Cacti need very little water. Water them once every 2-3 weeks.";
            } else if (userPlant === "fern") {
                wateringInfo = "Ferns like to be kept moist. Water them once a week.";
            } else if (userPlant === "bamboo") {
                wateringInfo = "Bamboo needs a lot of water. Water them every 2-3 days.";
            } else if (userPlant === "succulent") {
                wateringInfo = "Succulents need moderate water. Water them every 1-2 weeks.";
            } else if (userPlant === "orchid") {
                wateringInfo = "Orchids like to dry out between waterings. Water them every 1-2 weeks.";
            } else {
                wateringInfo = "Sorry, I don't have information on that type of plant.";
                response.className = "result error"; // Error class
            }
            // Update response section with the appropriate message
            response.className = "result water-info"; // Reset to default info
            response.innerHTML = wateringInfo;
        }
    </script>
<div>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
            color: #333;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #ffffff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            width: 300px;
            text-align: center;
        }
        h3 {
            color:rgb(33, 61, 34);
            font-size: 24px;
        }
        label {
            font-size: 16px;
            margin-bottom: 5px;
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
        #output {
            font-size: 18px;
            font-weight: bold;
            margin-top: 20px;
        }
        .result {
            padding: 10px;
            border-radius: 4px;
            margin-top: 10px;
        }
        .water-needed {
            background-color: #ffcccb; /* Light red */
            color: #d9534f; /* Red text */
        }
        .water-not-needed {
            background-color: #d4edda; /* Light green */
            color: #28a745; /* Green text */
        }
        .error {
            background-color: #f8d7da;
            color: #721c24;
        }
    </style>
<body>
    <div class="container">
        <h1>🌱 Plant Watering Reminder 🌱</h1>
        <label for="plantType">Plant Type:</label>
        <input type="text" id="plantType" placeholder="e.g., Cactus"><br>
        <label for="lastWatered">Last Watered (YYYY-MM-DD):</label>
        <input type="date" id="lastWatered"><br>
        <button onclick="checkWatering()">Check Watering Status</button>
        <h2 id="output"></h2>
    </div>
    <script>
        function checkWatering() {
            const plants = [
                {name: "Cactus", interval: 10},
                {name: "Fern", interval: 3},
                {name: "Orchid", interval: 7},
                {name: "Bamboo", interval: 2},
                {name: "Succulent", interval: 14}
            ];
            const plantType = document.getElementById("plantType").value.trim();
            const lastWatered = document.getElementById("lastWatered").value;
            const output = document.getElementById("output");
            if (!plantType || !lastWatered) {
                output.innerHTML = `<div class="result error">❌ Please enter both the plant type and the last watered date.</div>`;
                return;
            }
            const today = new Date();
            const lastDate = new Date(lastWatered);
            if (isNaN(lastDate)) {
                output.innerHTML = `<div class="result error">❌ Invalid date. Please enter a valid date.</div>`;
                return;
            }
            const daysSinceWatered = Math.floor((today - lastDate) / (1000 * 60 * 60 * 24));
            let found = false;
            for (let plant of plants) {
                if (plant.name.toLowerCase() === plantType.toLowerCase()) {
                    found = true;
                    if (daysSinceWatered >= plant.interval) {
                        output.innerHTML = `<div class="result water-needed">🌱 Your ${plant.name} needs watering! (${daysSinceWatered} days since last watered)</div>`;
                    } else {
                        output.innerHTML = `<div class="result water-not-needed">✅ Your ${plant.name} is fine. Only ${daysSinceWatered} days since last watered.</div>`;
                    }
                    break;
                }
            }
            if (!found) {
                output.innerHTML = `<div class="result error">❌ Sorry, that plant is not in our database.</div>`;
            }
        }
    </script>
</body>