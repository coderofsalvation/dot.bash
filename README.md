interactive bash toolbelt for webdevelopment hipsters

<img src="https://media.giphy.com/media/ZcqHDQUJm1nZC/giphy.gif" width="320"/>

## Usage

put this in `~/.bashrc`:

    [[ -t 0  ]] && { 
      source path/to/dot.bash 
      PS1="[\u@\H\[\033[34m\]\w]\[\033[0m\] \$(.gitbranch) \[\033[1;34m\]$ \[\033[0m\]" # optional
    }    

> NOTE: the optional lines will display gitbranch in prompt

# Why 

Bash equalivent of lodash/underscore for interactive purposes, plus:

* promote command stacking instead of writing oneliners

# .stick

    $ .push mongo 192.169.0.5:9999/foo --eval
    mongo $ db.foo.find({})

# .stick & .push & .pop 

Always keeps your prompt at the top. and allows you to type less (commandstacking):

*curl*:
    
    $ .stick
    $ .push curl -H 'Content-Type: application/json' --user admin:password -v 
    curl $ _ -X POST http://foo.com --data '{}'
    +  curl -H 'Content-Type: application/json' -v -X POST http://foo.com '{}'
    ..(curl output)..
 
*mongodb*:
 
    $ .stick 
    $ .push mongo 192.169.0.5:9999/foo --eval
    mongo $ db.foo.find({})

> NOTE: use `.pop` to remove the stacked command
> NOTE: type `_` to recall the stacked command 
> NOTE: type `.unstick` to undo stick-to-top-prompt

# .json.get

Evaluate a key-path from a json-file or string

    $ .json.get package.json repository.type 
    git 

    $ .json.get '{"foo":['one','two']}' foo.0
    one

# .pretty & .prettylines

    $ cat singleline.json | .pretty
    {
      "foo":"bar"
    }
    $ cat foo.json | .prettylines | .markdown
        1 {
        2   "foo":"bar"
        3 }

# .markdown
# .markdown.render
    
    $ cat foo.json | .prettylines | .markdown
    $ cat foo.json | .prettylines | .markdown | .wrap "# json ${USER} output\n\n%s' | .markdown.render > foo.html

# .wrap

wrap template around stdin & env-vars.

> NOTE: piped content is substituted by '%s'

compose simple json:

    $ foo=bar
    $ echo -n '{ "foo": "%s", "user":"${USER} ${foo}" }' > template.json
    $ date | .wrap "$(<template.json)" | .pretty
    {
       "user" : "foo bar",
       "date" : "Wed Dec 28 21:40:11 CET 2016"
    }

REST json-post:

    $ date | .wrap "$(<template.json)" | curl -X POST http://localhost:3000/ping -d @-

template > markdown > html:

    $ ls -la | .markdown | .wrap '# ls -la output\n\n%s ${USER}' | .markdown.render
    <h1>ls -la output</h1>
    <pre>
    total 757M
    drwx------  2 sqz  sqz  4.0K Dec 28 21:25 vbjdwRv
    drwxrwxrwt 33 root root  48K Dec 28 21:25 .
    drwx------  2 sqz  sqz  4.0K Dec 28 18:09 vZIos2X
    drwx------  2 sqz  sqz  4.0K Dec 28 17:15 vzwsR4d
    </pre>
    <p>
      Wed Dec 28 21:26:44 CET 2016 john
    </p>

# project scope:

* wrappers 
* small functions
* offline utilities  (with markdown as exception)
* make use of installed devlangs (python/perl/awk)
