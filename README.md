Sticky prompt for bash

<img src="https://media.giphy.com/media/ZcqHDQUJm1nZC/giphy.gif" width="320"/>

## Usage

put this in `~/.bashrc`:

    source path/to/sticky
    trap sticky_hook DEBUG

Then whenever you want your prompt to stick to the top:

    $ stick

And to unstick:

    $ unstick

