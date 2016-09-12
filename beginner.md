# Beginner track

This page shows a project
that is aimed at beginners.
It will carefully walk through the steps
required to make a functioning code project.

With this whole event,
please know that the organizers are here
to help people learn.
Learning tends to work best
when you think hard
about the problem at hand,
but if you truly get stuck,
let us know!

## Goal and overview

*Coding is the superpower of the 21st century.*

Our goal with this project is
to get you hands on experience with real code.
The project should demonstrate
how you can obtain this modern superpower
and apply it to your work, your learning, or your play.

Specifically,
we will show you how to get data sent right to your fingertips.
By the time you're done,
your code will send the weather
directly to you
via a text message.

Stop and think about that for a second.
Weather information collected from satellites
will be distilled down
into a bite size chunk of information.
That information will travel over the internet,
through datacenters,
fiber optic cables,
and wireless signals
to arrive specially packaged...
for you.
*Isn't that amazing!?*
We think so.

Let's get started, ok?

## Get ready to write code

We write code in a plain text format.
This has a very specific meaning for computers,
but suffice it to say
that to write in plain text,
we need a text editor.
If you know Windows,
Notepad is a text editor.
Microsoft Word is not a text editor;
it is a word processor,
and a powerful one to boot.

While it would be possible to use a simple program
like Notepad
to write code,
such simple tools are not well suited
for software development.

Instead,
we will use Sublime Text.
Sublime Text is a powerful text editor
meant for people who want to write code.
It includes great features
like syntax highlighting
that will make your work easier.

Download it from the
[Sublime Text website](https://www.sublimetext.com/)
and install it on your machine.

## Running commands

We need a way to tell the computer what to do.
To provide these instructions,
we'll use a program called a terminal.
A terminal goes by many names.
You might have heard of
a command line interface (CLI),
command prompt,
or a shell.
These are all (roughly) the same thing.
A terminal is a text based interface
where you type commands
that instruct your computer about what to do.

If you can't find the terminal
on your machine,
find an organizer to help
or ask a neighbor.

This guide will use a Linux style terminal
when showing examples.
A Linux style often uses a `$`
at the beginning of a line.
When you see these examples,
you do not need to type the `$`.
Here's a sample:

```bash
$ echo 'Hello World!'
Hello World!
```

That command told the computer
to repeat the content inside the quotation marks.

You will see a variety of different commands
by following this project.

## A home for your code

To get started,
let's make a place
where our code can reside.
Create a directory
with whatever name you want.
For this guide,
we'll call our project `hackathon`.

```bash
$ mkdir hackathon
$ cd hackathon
```

## Setup Python

All the code for this project
will use the Python programming language.
Python is an interpreted language.
This means that Python code
is given to an interpreter program,
and that program interprets (go figure!) the instructions
and runs them.
In contrast,
a language like C++ is considered a compiled language.
With a compiled language,
the code is given to a compiler program
which converts the code into a machine readable file
(that is, another program).
The distinction isn't very important for this project.
Practically,
it means that we don't have an extra step
of putting our code through a compiler first.
We get to run the code directly.

We're going to use Python 3.5.2.
There are a variety of ways to install Python.
If you don't already have Python installed,
grab the installer from the
[Python downloads page](https://www.python.org/downloads/)
and install it on your machine.

Let's discuss your development environment
for a moment.
At this point,
your machine should have Python installed on it.
An installation of Python is, in reality, at least two things.
The core part is the interpreter
that can run code.
The secondary part is a massive standard library
of additional code
that can help you do cool stuff.
This library of code helps
so that you don't have to write all the tools yourself.
One of Python's mottos is "batteries included,"
and the standard library is the batteries.

But the internet is full of *even more* cool stuff.
People from all over the world contribute additional code
that won't fit in the standard library.
This code is "packaged" into packages
that we can install on our machines.
Python provides a tool to get access to those packages.
That tool is
[pip](https://pip.pypa.io/en/stable/).

Before moving on to using `pip`,
there is one more thing to consider.
When Python was installed,
your operating system
(a.k.a. Windows, OS X, or Linux)
put the Python files
in a special location
on your machine.
That installation may have required special administrative privileges
to work.
When adding packages
from the internet
with `pip`,
we want to avoid needing those privileges.
We want a sandbox
where our extra packages can live
without interferring with other parts
of the operating system.

In Python-land,
these sandboxes are called virtual environments
(to maximize the amount of jargon to learn :smile:).
Modern versions of Python include `pyvenv`,
a tool to create virtual environments.
Let's make one.

```bash
$ pyvenv venv
```

There should be a new directory, `venv`,
in your project area
that is full of stuff.
Before the terminal will use that virtual environment,
you must activate it.

```bash
$ source venv/bin/activate
```

Windows users can activate their virtual environment
using a different command.
Check out the
[Python venv documentation](https://docs.python.org/3/library/venv.html#creating-virtual-environments)
for details.

Note:
some commands will differ
between Windows and OS X and Linux.
Where the differences are large,
we will try to call them out.

## Optional side quest: add version control to your project

Version control is a key tool
for sharing your project
and protecting it from loss.
Read about
[adding version control](version_control.md)
if you would like.

## Set up project

We need some weather data to use.
There are *tons* of weather data services,
and [OpenWeatherMap](http://openweathermap.org/)
is the service we selected.
This service is free
for the amount of data we plan to fetch from the site.

To use their data,
you must create an account through their website.

TODO: Nexmo

All the data that we are receiving and sending
is going over the internet.
There is a very nice package
that is not part of the standard library
that will make our efforts much easier.
The package,
[requests](http://requests.readthedocs.io/en/master/),
will help us get and send on the internet.
Install it with `pip`.

```bash
$ pip install requests
```

## Intro to APIs

You ready to write some code?
We've finally arrived.
With all of the setup complete,
we can get to the task at hand.

When working with OpenWeatherMap and Nexmo,
we will use APIs.
API is short for Application Programming Interface.
An API describes how code can interact
with external services
and collect or send data.

### OpenWeatherMap

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

Let's switch gears
and take a close look at the Nexmo API.

### Nexmo

TODO: Nexmo

## Connecting things together

TODO: code

## Next steps
