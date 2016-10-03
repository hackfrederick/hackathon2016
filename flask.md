---
layout: default
permalink: /flask/
---

# Flask

Next we might want a web server that we can view the data from.  
Using Flask we can set that up very easily.  

Before starting we will want to setup a virtual environment.

```bash
virtualenv .
. ./bin/activate
```

Then we will want to make sure we install flask and requests

```bash
pip install flask
pip install requests
```

Create the app by running

```bash
touch app.py
```

Then edit the app.py with the following:

```python
from flask import Flask
from flask import jsonify
import requests
from datetime import datetime

app = Flask(__name__)

def icon(icon_id):
  fullpath = 'http://openweathermap.org/img/w/%s.png' % icon_id
  img = requests.get(fullpath)
  return img

def weather():
  params = {
      'q': 'Frederick, MD',
      'appid': '6022e29b03c12bf2a1d7daa527cf98c4',
  }

  response = requests.get(
      'http://api.openweathermap.org/data/2.5/weather', params=params)

  weather_data = response.json()
  weather_data['time'] = datetime.now()
  return weather_data

@app.route('/')
def main():
  weather_data = weather()
  return jsonify(weather_data)

@app.route('/image')
def image():
  weather_data = weather()
  image = icon(weather_data['weather'][0]['icon'])
  return Flask.response_class(image, mimetype='image/png')
```

You will notice that the weather function looks familiar. We are adding a
path generator that builds a path to pull the openweathermap.org's icon
image for each weather event. It uses the requests package to pull the image
and then presents it to the user when the /image route is hit.

To run the app do the following:

```bash
export FLASK_APP=app.py
flask run
```

Open your browser and go to http://localhost:5000

You will see the following.

```json
{
  "base": "stations", 
  "clouds": {
    "all": 0
  }, 
  "cod": 200, 
  "coord": {
    "lat": 39.41, 
    "lon": -77.41
  }, 
  "dt": 1475443439, 
  "id": 4355585, 
  "main": {
    "humidity": 71, 
    "pressure": 1015, 
    "temp": 294.98, 
    "temp_max": 296.48, 
    "temp_min": 293.71
  }, 
  "name": "Frederick", 
  "rain": {
    "1h": 0.1
  }, 
  "sys": {
    "country": "US", 
    "id": 9537, 
    "message": 0.2462, 
    "sunrise": 1475406482, 
    "sunset": 1475448501, 
    "type": 3
  }, 
  "time": "Sun, 02 Oct 2016 17:35:21 GMT", 
  "weather": [
    {
      "description": "light rain", 
      "icon": "10d", 
      "id": 500, 
      "main": "Rain"
    }
  ], 
  "wind": {
    "deg": 201.002, 
    "speed": 2.05
  }
}
```

Then go to http://localhost:5000/image. You will see a small icon that 
represents the current weather. 
