# Weather Data Fetching with OpenWeatherMap API

This repository demonstrates how to interact with the [OpenWeatherMap API](https://openweathermap.org/api) using **cURL**, **Postman**, and **Python**. This project is aimed at helping developers understand how to use APIs to fetch weather data and process the response.

## Overview

This project fetches the current weather data for a specified location (Delhi, in this case) using the OpenWeatherMap API. The data is retrieved in JSON format, displaying details like temperature, humidity, weather conditions, wind speed, and more.

## Contents

- **cURL Request**: Command-line approach to fetch weather data.
- **Postman Setup**: Using Postman to test the API.
- **Python Script**: Programmatic way to interact with the API and process the JSON response.

## Prerequisites

To follow along with this repository, you will need:
- [Python 3](https://www.python.org/downloads/) installed on your system.
- A free API key from [OpenWeatherMap](https://home.openweathermap.org/users/sign_up).
- (Optional) [Postman](https://www.postman.com/downloads/) for testing API requests.

## Getting Started

### 1. Set Up Your OpenWeatherMap API Key

1. Sign up at [OpenWeatherMap](https://home.openweathermap.org/users/sign_up) and log in.
2. Generate an API key from the [API keys section](https://home.openweathermap.org/api_keys).
3. Copy the API key; you will need it to authenticate your requests.

### 2. Testing with cURL

Use the following cURL command to fetch the weather data for Delhi:

```bash
curl --ssl-no-revoke -X GET "https://api.openweathermap.org/data/2.5/weather?q=Delhi&appid=YOUR_API_KEY"
```

Replace `YOUR_API_KEY` with your actual API key.

### 3. Testing with Postman

1. Open Postman and create a new GET request.
2. Enter the URL:
   ```
   https://api.openweathermap.org/data/2.5/weather?q=Delhi&appid=YOUR_API_KEY
   ```
3. Replace `YOUR_API_KEY` with your actual key.
4. Click **Send** to see the JSON response.

### 4. Using the Python Script

A simple Python script, `weather_api_test.py`, is included to demonstrate how to interact with the OpenWeatherMap API programmatically.

#### Python Script (`weather_api_test.py`)

```python
import requests

# Replace YOUR_API_KEY with your actual OpenWeatherMap API key
api_key = "YOUR_API_KEY"
city = "Delhi"
url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}"

# Make the GET request
response = requests.get(url)

# Check if the request was successful
if response.status_code == 200:
    data = response.json()  # Parse the JSON response
    print("Weather Data for Delhi:")
    print(data)  # Display the raw JSON data

    # Extract specific information
    temperature = data["main"]["temp"]
    weather = data["weather"][0]["description"]
    print(f"Temperature: {temperature}K")
    print(f"Weather Description: {weather}")
else:
    print(f"Failed to retrieve data. Status code: {response.status_code}")
```

### Running the Script

1. Save the script in your project directory as `weather_api_test.py`.
2. Open a terminal in the directory and run:

   ```bash
   python weather_api_test.py
   ```

3. The script will display the current weather data for Delhi.

## Example Output

Below is an example of the JSON response retrieved:

```json
{
    "coord": {"lon": 77.2167, "lat": 28.6667},
    "weather": [{"id": 721, "main": "Haze", "description": "haze", "icon": "50n"}],
    "main": {
        "temp": 296.2,
        "feels_like": 296.34,
        "pressure": 1013,
        "humidity": 68
    },
    "wind": {"speed": 0, "deg": 0},
    "clouds": {"all": 0},
    "sys": {"country": "IN"},
    "name": "Delhi",
    "cod": 200
}
```

## Notes

- **Temperature** is provided in Kelvin by default; you can convert it to Celsius by subtracting 273.15.
- You can change the `city` parameter in the Python script or in the cURL command to fetch data for other locations.

## Resources

- [OpenWeatherMap API Documentation](https://openweathermap.org/api)
- [Python Requests Library](https://docs.python-requests.org/)

## License

This project is licensed under the MIT License.
