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

The other major component
is a service to send text messages.
[Nexmo](https://www.nexmo.com/),
our sponsor,
provides such a service
for us to use.

To send SMS messages,
you must create an account through their website.

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
to collect or send data.

[Start with the weather](open_weather_map.md).

[Then check out Nexmo](nexmo.md).

[Finally, put them together](connecting.md).

## Next steps

If you got through everything,
it's time to kick in some creativity.
[Grab some ideas and get going](next.md).
