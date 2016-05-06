
Sticky prompt for bash

<img src="https://media.giphy.com/media/ZcqHDQUJm1nZC/giphy.gif" width="320"/>

## Usage

put this in `~/.bashrc`:

    alias sticky="source path/to/sticky"

Then whenever you want your prompt to stick to the top:

    $ sticky

And to unstick:

    $ unsticky

## OSX note:

osx iterm2-users only:

  * open preferences (applekey+,)
  * uncheck 'Insert newline before start of command prompt if needed' in the Terminal-tab
