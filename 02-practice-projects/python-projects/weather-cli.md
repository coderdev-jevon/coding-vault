# Weather CLI
Date: 2026-07-31
## Lessons
1. -
## * How to Use API

1. Think API as a waiter, it takes order from you and brings you the food back
2. **Request URL Structure**
? is the start of the parameters
**Key** works as authentication, prove that you are allowed
```
BASE_URL ? parameter1=value & parameter2=value

https://api.weatherapi.com/v1/current.json?key=YOUR_KEY&q=Jakarta
```
3. Server returns JSON text and status codes
```python
response.json()
response.raise_for_status() #really important to send errors from the server
```

#### ** Step by step
	Find API from website -> get base url and key -> run to the code
Example:
```python
import requests

API_KEY = "ce23e409e48a4dc5b1f74944263107"
url = "https://api.weatherapi.com/v1/current.json"

# Step 1: define parameters we send, why payload? it is like the cargo you sent to the server
payload = {
    "key": API_KEY,
    "q": "Jakarta"
}

# Step 2: send GET request to server
response = requests.get(url, params=payload, timeout=10)

# Step3: check if request succeeded
response.raise_for_status()

# Step4: convert JSON response into Python dictionary
weather_data = response.json()

# Step5: extract information from dictionary
city_name = weather_data["location"]["name"]
temperature = weather_data["current"]["temp_c"]

print(f"{city_name}: {temperature}°C")
```

#### ** Common Issues
	No internet -> ConnectioNError, Slow internet -> Timeout, Wrong city name -> 400 error, KeyError


#project #api #errors  #requests #