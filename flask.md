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
