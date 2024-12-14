---
tags:
- python
---

## **Python Phone Number Tracking Project**

### Project Overview

This Python project creates a program to track a phone number's location and display it on Google Maps. The project uses several libraries, including `phone_numbers` for parsing phone information, `OpenCage` for geolocation, and `folium` to render a map.

---

### Project Setup

1. **Create Project Files**:

    - Open your code editor and create a new folder named `track_location`.
    - Inside the folder, create two Python files:
        - `main.py`: This file will contain the main code to execute the tracking.
        - `my_phone.py`: This file will store the phone number to be tracked.

2. **Set Up** `**my_phone.py**`:

    - In `my_phone.py`, define a variable for the phone number:

        ```
        number = "<your_phone_number>"  # Replace <your_phone_number> with the actual phone number.
        ```

---

### Install Required Packages

- Open your terminal and install the following packages:

    ```bash
    pip install phone_numbers
    pip install opencage
    pip install folium
    ```

---

### Code for `main.py`

1. **Import Necessary Libraries**:

    ```python
    import phone_numbers
    from my_phone import number
    from phone_numbers import geocoder, carrier
    from opencage.geocoder import OpenCageGeocode
    import folium
    ```

2. **Define API Key for OpenCage**:

    - Sign up at [OpenCageData](https://opencagedata.com) to get a free API key.
    - Add your API key in `main.py`:

        ```python
        key = "YOUR_API_KEY"  # Replace with your actual OpenCage API key
        geocoder = OpenCageGeocode(key)
        ```

3. **Extract Country and Service Provider Information**:

    - Use the `phone_numbers` library to parse the phone number and extract details.

    ```python
    parsed_number = phone_numbers.parse(number)
    location = geocoder.description_for_number(parsed_number, "en")
    service_provider = carrier.name_for_number(parsed_number, "en")
    
    print("Country:", location)
    print("Service Provider:", service_provider)
    ```

4. **Get Coordinates Using OpenCage**:

    - Use OpenCage to fetch the latitude and longitude of the phone number’s country:

    ```python
    query = str(location)
    results = geocoder.geocode(query)
    latitude = results[0]['geometry']['lat']
    longitude = results[0]['geometry']['lng']
    
    print("Latitude:", latitude)
    print("Longitude:", longitude)
    ```

5. **Render Location on Google Map**:

    - Use `folium` to create a map with the phone’s approximate location.

    ```python
    my_map = folium.Map(location=[latitude, longitude], zoom_start=9)
    folium.Marker([latitude, longitude], popup=location).add_to(my_map)
    
    # Save map to HTML
    my_map.save("my_location.html")
    ```

6. **Run the Program**:

    - Run `main.py` to generate a file `my_location.html` containing the map.
    - Open this file in your browser to view the location on Google Maps.

---

### Complete Code for `main.py`

```python
import phone_numbers
from my_phone import number
from phone_numbers import geocoder, carrier
from opencage.geocoder import OpenCageGeocode
import folium

# Initialize OpenCage API key
key = "YOUR_API_KEY"  # Replace with your actual OpenCage API key
geocoder = OpenCageGeocode(key)

# Parse and get details of the phone number
parsed_number = phone_numbers.parse(number)
location = geocoder.description_for_number(parsed_number, "en")
service_provider = carrier.name_for_number(parsed_number, "en")

# Print country and service provider
print("Country:", location)
print("Service Provider:", service_provider)

# Get latitude and longitude for map rendering
query = str(location)
results = geocoder.geocode(query)
latitude = results[0]['geometry']['lat']
longitude = results[0]['geometry']['lng']

# Print latitude and longitude
print("Latitude:", latitude)
print("Longitude:", longitude)

# Create map and add marker
my_map = folium.Map(location=[latitude, longitude], zoom_start=9)
folium.Marker([latitude, longitude], popup=location).add_to(my_map)

# Save map to HTML
my_map.save("my_location.html")
```

---

### Usage Notes

- **Privacy**: Ensure you have permission to use and track the phone number.
- **Location Accuracy**: This approach provides a general location based on country and service provider and is not suitable for precise real-time tracking.
- **API Limits**: OpenCage may have usage limits for free accounts.

[[Python]]