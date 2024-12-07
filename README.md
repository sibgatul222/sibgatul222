import requests
import sys

def get_weather(city):
    # API endpoint and your API key (you can get it from OpenWeatherMap API)
    api_key = "your_api_key_here"
    base_url = "http://api.openweathermap.org/data/2.5/weather?"

    # Complete URL
    complete_url = f"{base_url}q={city}&appid={api_key}&units=metric"

    # Make the request to OpenWeatherMap API
    response = requests.get(complete_url)

    # Convert response to JSON
    data = response.json()

    # If the response code is 200, the city is found
    if data["cod"] == "404":
        print(f"City {city} not found!")
    else:
        # Extracting the main data
        main = data["main"]
        temperature = main["temp"]
        pressure = main["pressure"]
        humidity = main["humidity"]

        # Extracting the weather description
        weather = data["weather"]
        weather_description = weather[0]["description"]

        # Displaying the weather information
        print(f"Weather in {city}:")
        print(f"Temperature: {temperature}°C")
        print(f"Pressure: {pressure} hPa")
        print(f"Humidity: {humidity}%")
        print(f"Description: {weather_description.capitalize()}")
    
def main():
    # Ask user for the city name
    city = input("Enter city name: ")
    get_weather(city)

if __name__ == "__main__":
    main()
