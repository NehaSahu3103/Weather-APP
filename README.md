<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background: #f0f8ff;
        }
        .container {
            text-align: center;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 350px;
        }
        input {
            padding: 12px;
            margin: 10px auto;
            border: 1px solid #ccc;
            border-radius: 5px;
            display: block;
            width: 90%;
            font-size: 18px;
        }
        button {
            padding: 10px;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: block;
            width: 60%;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
        }
        button:hover {
            background: #0056b3;
        }
        .weather-info {
            margin-top: 20px;
            text-align: center;
            padding: 15px;
            border-radius: 5px;
            background: #eef6ff;
            width: 90%;
            display: inline-block;
        }
        .weather-info p {
            margin: 10px 0;
            font-size: 18px;
        }
        .weather-info p strong {
            font-weight: bold;
        }
        h2 {
            font-size: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Weather App</h1>
        <input type="text" id="location" placeholder="Enter location">
        <button onclick="getWeather()">Get Weather</button>
        <div class="weather-info" id="weather"></div>
    </div>
    
    <script>
        async function getWeather() {
            const location = document.getElementById('location').value;
            const apiKey = '7a0518942f1e4bc5ae0130647252602';
            const url = `http://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${location}&aqi=yes`;
            
            try {
                const response = await fetch(url);
                const data = await response.json();
                
                if (data.error) {
                    document.getElementById('weather').innerHTML = `<p style="color: red; font-size: 16px;">${data.error.message}</p>`;
                    return;
                }
                
                const weatherHtml = `
                    <h2><strong>Location:</strong> ${data.location.name}, ${data.location.country}</h2>
                    <p><strong>Temperature:</strong> ${data.current.temp_c}°C</p>
                    <p><strong>Condition:</strong> ${data.current.condition.text}</p>
                    <img src="${data.current.condition.icon}" alt="Weather Icon">
                `;
                document.getElementById('weather').innerHTML = weatherHtml;
            } catch (error) {
                document.getElementById('weather').innerHTML = `<p style="color: red; font-size: 16px;">Failed to fetch weather data</p>`;
            }
        }
    </script>
</body>
</html>
