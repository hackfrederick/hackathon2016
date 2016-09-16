---
layout: default
permalink: /connecting/
---

# Connecting the services together

It's time to show off your superpowers.
We have our `weather_data`
and we have the ability
to send a text message.
Now we must pull out some weather data,
make a pleasant message out of it,
and send to our phones.

So far,
we pretty printed the weather data
to the terminal,
but we didn't extract anything from the data.

In case you forgot,
here's what our weather data looks like:

```bash
$ python weather_service.py
{'base': 'stations',
 'clouds': {'all': 1},
 'cod': 200,
 'coord': {'lat': 39.41, 'lon': -77.41},
 'dt': 1473909937,
 'id': 4355585,
 'main': {'humidity': 61,
          'pressure': 1020,
          'temp': 74.64,
          'temp_max': 78.8,
          'temp_min': 71.01},
 'name': 'Frederick',
 'sys': {'country': 'US',
         'id': 2856,
         'message': 0.0437,
         'sunrise': 1473936686,
         'sunset': 1473981424,
         'type': 1},
 'visibility': 16093,
 'weather': [{'description': 'clear sky',
              'icon': '01n',
              'id': 800,
              'main': 'Clear'}],
 'wind': {'deg': 20, 'speed': 9.17}}
```

That's complicated
so let's break it down.
The data is wrapped in curly braces
so that tells us that the entire response
is a big Python dictionary.

The words along the left side
are the keys
for that dictionary.
But what is going on with the values on the right side?
`'stations'`?
`{'all': 1}`?
`200`?
It seems to make no sense
until you learn
that Python dictionary values do not have to be the same type of data.
Now is also a good time to observe
that a Python dictionary value can be **another dictionary**.
A dictionary that is a value
of a dictionary
is often called a *nested* dictionary.

Imagine reading a book
with a footnote,
and the footnote says to go read another book
for a detailed explanation.
It's kind of like that.

We access data
in a dictionary
using square brackets
and a key.

```python
city = weather_data['name']
print(city)
```

For our message,
let's display the temperature.
The temperature is in a nested dictionary
so we need to use keys
from both the outer dictionary
and the nested one.

You could write this a couple of ways:

```python

main_data = weather_data['main']
temperature = main_data['temp']

# Or, like this...

temperature = weather_data['main']['temp']
print(temperature)
```

With a city and temperature,
we can build a reasonable message
using formatting.

```python
message = 'The weather in {} is {} degrees Fahrenheit.'.format(city, temperature)
print(message)
```

Using `format`,
we can put our extracted data
into a nice message.
You can probably guess how `format` works.
`format` will look
at the words in quotes,
find the curly brace pairs,
and replace them
with data
that is provided.

Aside:
data that is put in quotes
is called a "string"
in programming languages.
We've avoided calling them strings so far
because it's not strictly necessary to know,
but if you continue down the path
of programming,
"string" will be a word
that you need to know.
How about that?
Now you *do* know what that means.

With the `message` prepared,
put it in your Nexmo API code:

```python
    'text': message,
```

Run your code to see the results!
Don't you feel super?

![Super Duper.](http://i.giphy.com/l2Sq9mzrjHG39i0i4.gif)

What's next?
[Time to get creative](next.md).
