## Add version control to your project

You should know of an important concept called version control.
Version control is a safety net if you mess up badly.

TODO: teach the merits of version control and direct to GitHub
TODO: create GitHub account
TODO: set up Git config

```bash
$ git init .
```

Some files do not need version control.
In fact,
some files can even cause trouble
for other users
if you are collaborating
on your project.
The virtual environment is a good example.
The virtual environment on your computer
may have code that will only work
on your computer.
If you are working on OS X
and your partner is on Windows,
then the differences
in virtual environments
will create trouble.
Git provides a way to ignore certain files or directories.
To do this,
we can use a `.gitignore` file.
Git will check this file
and ignore anything that matches.
We can ignore the virtual environment
by creating our `.gitignore` file
with `venv` as the initial content.

```bash
$ echo 'venv' > .gitignore
```

For files that we do want,
we need to tell Git that we want them.
Let's add our `.gitignore` file.

```bash
$ git add .gitignore
```

Now we must commit the changes.
A commit acts as a checkpoint
for our project.
Every time you commit code,
Git will remember the state
of the entire project.
Navigating commit history
is how we can travel back in time
and recover from mistakes we make.

```bash
$ git commit -m 'First commit!'
```

Learning the ins and outs of Git
would take a very long time,
but knowing this much can save a project
from catastrophe.

To get your project on GitHub,
check out
[their help documentation](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/).
