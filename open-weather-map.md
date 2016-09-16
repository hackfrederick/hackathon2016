---
layout: default
permalink: /open-weather-map/
---

# OpenWeatherMap

We can start
by looking at the
[OpenWeatherMap API](http://openweathermap.org/current).

The page tells us
that we can get the current weather
by doing a web request to something like:
`api.openweathermap.org/data/2.5/weather?q=London,uk`

There are two things to note about this:

1. The documentation fails to tell us
   to include `http://`
   in front of the request.
   This is something experienced developers
   are likely to know,
   but it can bite somebody new to coding.
   HTTP stands for Hypertext Transfer Protocol
   and is the most common protocol used to exchange information
   over the internet.
2. What's the deal with `q`?
   In this case,
   `q` is short for "query"
   so this example request is asking
   "what is the current weather in London, UK?"

Can we get an answer?
Start by creating a file in your project directory
named `weather_service.py`.

```bash
$ touch weather_service.py
```

Open that file in Sublime.
It should be empty.
The first thing to do is to tell Python
that we want to use the `requests` package
that we installed.

```python
# This is a comment (which is a line that Python will ignore
# when running). A comment is any line that starts with a #.
# You can use comments to explain things in your code.
# For instance, this file is weather_service.py.

import requests
```

Next, let's tell `requests` to get the data
from the internet.

```python
response = requests.get('http://api.openweathermap.org/data/2.5/weather?q=London,uk')
```

Now we can run that code.

```bash
$ python weather_service.py
```

What!?
Nothing happened.
Yep,
something did happen,
but we did not see the results.
The command that we ran
told the Python interpreter
to read the code in `weather_service.py`
and run those instructions.
Assuming we typed everything correctly,
`requests` went out to the internet,
got an answer from OpenWeatherMap,
and stored it in `response`.
The problem is that we didn't tell Python
to show us the results.
For that,
we can use `print`.
Add a `print` to the bottom of the file.

```python
print(response.text)
```

Try it again.

```bash
$ python weather_service.py
{"cod":401, "message": "Invalid API key. Please see http://openweathermap.org/faq#error401 for more info."}
```

Huh?
That doesn't look like weather data.
An important lesson
in this process
is that coding is about taking small steps.
Each little step reveals some new part
of the puzzle.
We'll get to an answer soon enough.
That FAQ page says
we need to use `APPID` for access.
The `APPID` is the key
you can find at
[your account's API key page](https://home.openweathermap.org/api_keys).

Now we can change our code to use that key.

```python
response = requests.get('http://api.openweathermap.org/data/2.5/weather?q=London,uk&appid=<your API key here>')
```

Try again.

```bash
$ python weather_service.py
{"coord":{"lon":-0.13,"lat":51.51},"weather":[{"id":800,"main":"Clear","description":"clear sky",
"icon":"01n"}],"base":"stations","main":{"temp":286.42,"pressure":1015,"humidity":63,"temp_min":283.15,
"temp_max":290.15},"visibility":10000,"wind":{"speed":2.1,"deg":190},"clouds":{"all":0},"dt":1473629602,
"sys":{"type":1,"id":5091,"message":0.0423,"country":"GB","sunrise":1473571860,"sunset":1473618079},
"id":2643743,"name":"London","cod":200}
```

**Sweet success!**

We now have some data
from OpenWeatherMap,
but there is some good opportunity
for clean up
before we move on.
We are going to do something
that developers like to call "refactoring."
Refactoring involves making changes to code
without changing the behavior
(that is, the outcome).
Look at the web address
of the request.
It's kind of unwieldy.
The web address,
which is also known as a URL,
has a well defined format.
Everything after the `?` character
are called parameters.
Because many APIs deal with parameters,
`requests` provides a nicer way
of handling them in your code.
We can change the code to look like the following:

```python
params = {
    'q': 'London,uk',
    'appid': '<your API key here>',
}
response = requests.get('http://api.openweathermap.org/data/2.5/weather', params=params)
```

If you run this again,
you can see that this code is functionally the same as the original.
This clean up is nice
because we now have one place
that can add more parameters
without the URL growing to be a mile long.

That `params` that you made is Python dictionary.
Think of a Python dictionary
like you would think of a regular dictionary.
With a dictionary,
you look up a word
and find its definition.
With a Python dictionary,
you look up a `key`
and find its `value`.
In `params`,
`q` and `appid` are the keys,
and `London,uk` and `<your API key here>` are the values.
Python dictionaries are a very useful way to store data
in your code.

Time to think about the output.
That mess of data that we saw
certainly had important information in it,
but it was a pain to decipher.
What was saw was the raw data
that came in the response.
Maybe you noticed
that the data had some patterns
and repeating characters in it.
What is that?
That is
[JSON](http://json.org/).
JSON is a format
used by many APIs
that structures data
in an approachable way.
One way we can think of JSON is as a dictionary.
In fact,
`requests` let's us do exactly that.
Change your `print` statement
to the following:

```python
print(response.json())
```

Let's look at the output now:

```bash
$ python weather_service.py
{'cod': 200, 'weather': [{'main': 'Clear', 'description': 'clear sky', 'icon': '01n', 'id': 800}],
 'id': 2643743, 'name': 'London', 'dt': 1473640478, 'sys': {'country': 'GB', 'type': 1,
 'sunrise': 1473658272, 'message': 0.0105, 'sunset': 1473704462, 'id': 5091}, 'wind': {'speed':
 2.1, 'deg': 120}, 'clouds': {'all': 0}, 'coord': {'lon': -0.13, 'lat': 51.51}, 'main':
 {'temp_min': 282.04, 'temp': 286.06, 'humidity': 72, 'pressure': 1015, 'temp_max': 291.15},
 'base': 'cmc stations'}
```

What we see still doesn't look very good.
Rest assured,
it is different.
Previously,
we were looking at the raw data
from OpenWeatherMap.
When we switched to using `json()`,
we told `requests` to convert the data
into a Python dictionary.
It might help to refactor the code
to get a clear name for our data
so we can talk about it.

```python
weather_data = response.json()
print(weather_data)
```

What can we do with this now that it's a Python dictionary?
We can use a pretty printer.
The standard libary comes with a pretty printer
called `pprint`.
Add the `pprint` module to the top of your file.

```python
import pprint
```

Change your `print` line to look like:

```python
pprint.pprint(weather_data)
```

How does this look?

```bash
$ python weather_service.py
{'base': 'cmc stations',
 'clouds': {'all': 0},
 'cod': 200,
 'coord': {'lat': 51.51, 'lon': -0.13},
 'dt': 1473640478,
 'id': 2643743,
 'main': {'humidity': 72,
          'pressure': 1015,
          'temp': 286.06,
          'temp_max': 291.15,
          'temp_min': 282.04},
 'name': 'London',
 'sys': {'country': 'GB',
         'id': 5091,
         'message': 0.0105,
         'sunrise': 1473658272,
         'sunset': 1473704462,
         'type': 1},
 'weather': [{'description': 'clear sky',
              'icon': '01n',
              'id': 800,
              'main': 'Clear'}],
 'wind': {'deg': 120, 'speed': 2.1}}
```

**Yeah, buddy!**

We have a fighting chance of seeing the kind of data
provided by OpenWeatherMap.

First,
let's change our location.
London's cool and all,
but this is Hack *Frederick*.

```python
params = {
    'q': 'Frederick,US',
    'appid': '<your API key here>',
}
```

Second,
look at the `temp`.
The high 200s doesn't seem right.
Jump back to the API documentation
and you will find information
about the data format.
By default,
OpenWeatherMap reports data
in Kelvins.
How, uh, *scientific* of them.
We need some Imperial units up in here.

![You know dat's right](http://i.giphy.com/QduCyLuNQYwpO.gif)

```python
params = {
    'q': 'Frederick,US',
    'appid': '<your API key here>',
    'units': 'imperial',
}
```

```bash
$ python weather_service.py
{'base': 'cmc stations',
 'clouds': {'all': 5},
 'cod': 200,
 'coord': {'lat': 39.41, 'lon': -77.41},
 'dt': 1473642249,
 'id': 4355585,
 'main': {'humidity': 73,
          'pressure': 1020,
          'temp': 70.3,
          'temp_max': 77,
          'temp_min': 64.76},
 'name': 'Frederick',
 'sys': {'country': 'US',
         'id': 1330,
         'message': 0.0105,
         'sunrise': 1473677315,
         'sunset': 1473722526,
         'type': 1},
 'weather': [{'description': 'clear sky',
              'icon': '02n',
              'id': 800,
              'main': 'Clear'}],
 'wind': {'speed': 3.36}}
```

That's way better.
70.3F and clear skies!
What am I doing inside writing this guide!? :wink:

Now let's switch gears
and
[take a close look at the Nexmo API](nexmo.md).
