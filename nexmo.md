---
layout: default
permalink: /nexmo/
---

# Nexmo

After walking through all the weather service work,
this section is going to feel like a walk in the park.
Why?
Because almost everything you did there
will apply here.
The primary differences are the URL
and data values to use.

Before starting,
you may want to "comment out"
your weather API code.
Comments start with `#`
and *anything* can appear
in a comment line.
For instance,
if you had code like

```python
print('Hello World')
```

and changed it to

```python
# print('Hello World')
```

then that `print` would no longer run
when you run your code.

By commenting out your weather API code,
you can stop it from running
and focus completely on the Nexmo code.

Your Nexmo account will point you to their
[Getting Started Guide](https://dashboard.nexmo.com/getting-started-guide).
Right from the start,
Nexmo provides an example command to run.

```bash
$ curl "https://rest.nexmo.com/sms/json?api_key=<your key>
&api_secret=<your secret>&from=<your from number>&to=<your to number>
&text=Welcome+to+Nexmo"
```

In this example,
`curl` is used.
`curl` is a terminal program
that can get stuff on the internet.
This one line will send a message
to the phone number specified after `to=`.

If we break this down,
we can tell that this is a URL
with a bunch of parameters.
We should be able to translate the URL
into our Python code.
Recall that everything after the question mark
is a parameter.
Also,
parameters are separated by an ampersand symbol.
Back in your Python code,
this request looks like:

```python
params = {
    'api_key': '<your key>',
    'api_secret': '<your secret>',
    'from': '<your from number>',
    'to': '<your to number',
    'text': 'Welcome+to+Nexmo',
}
requests.get('https://rest.nexmo.com/sms/json', params=params)
```

Something is a little strange about that.
What's up with the `+` symbols
between the words?
That's required
for URLs when there is a space character.
But guess what?
`requests` totally handles that for us
without you needing to do anything!
We can change the `text` line.

```python
    'text': 'Welcome to Nexmo',
```

You ready for this? That's it!
Run your code
and the receiving phone number should receive
a "Welcome to Nexmo" SMS message
after some amount of time.

With that,
it's time to
[glue the services together]({{ site.github.url }}/connecting/).

![Yum.](http://i.giphy.com/bnDMWYC4nzzO0.gif)
