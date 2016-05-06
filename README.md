
Sticky prompt for bash

<img src="https://media.giphy.com/media/ZcqHDQUJm1nZC/giphy.gif" width="320"/>

## Usage

put this in `~/.bashrc`:

    source path/to/sticky

Then whenever you want your prompt to stick to the top:

    $ stick

And to unstick:

    $ unstick

## OSX note:

osx iterm2-users only, after typing `stick` on 1st time run:

  $ trap pre_cmd DEBUG

not sure why this is needed
