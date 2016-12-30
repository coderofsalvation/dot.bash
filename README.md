interactive bash toolbelt for webdevelopment hipsters

<img src="https://media.giphy.com/media/ZcqHDQUJm1nZC/giphy.gif" width="320"/>

## Usage

put this in `~/.bashrc`:

    [[ -t 0  ]] && { 
      source path/to/dot.bash 
      PS1="[\u@\H\[\033[34m\]\w]\[\033[0m\] \$(.gitbranch) \[\033[1;34m\]$ \[\033[0m\]" # optional
    }    

> NOTE: the optional lines will display gitbranch in prompt

# .pretty 

    $ cat singleline.json | .pretty
    {
      "foo":"bar"
    }
    $ cat foo.json | .linenumbers | .markdown
        1 {
        2   "foo":"bar"
        3 }

# .wrap

wrap template around stdin & env-vars.

> NOTE: piped content is substituted by '%s'

compose simple json/xml or markdown on the fly:

    $ ls -la | .wrap '{"output":"%s"}'   | .pretty 
    $ date   | .wrap "$(<template.json)" | .pretty

# .json.post/put/delete/options 

    $ date | .json.post http://foo.com 
    $ echo '{"foo":"bar"}' | .json.put http://foo.com
    $ cat foo.json | .json.put http://foo.com 
    $ echo '{}' | .json.put http://foo.com/resource/32

# .json.path

Evaluate a key-path from a json-file or string

    $ .json.path package.json repository.type 
    git 

    $ .json.path '{"foo":['one','two']}' foo.0
    one


# .markdown & .markdown.render
    
    $ cat foo.json | .prettylines | .markdown
    $ cat foo.json | .prettylines | .markdown | .wrap "# json ${USER} output\n\n%s' | .markdown.render > foo.html


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

# .stick & .push & .pop 

Always keeps your prompt at the top (.stick). and type less using commandstacking (push/pop):

Finally use the bash recursive-search in poor REPL's:
 
    $ .stick 
    $ .push mongo 192.169.0.5:9999/foo --eval
    mongo $ _ db.foo.find({})                 

every command will be prepended with the pushed command
 
> NOTE: use `.pop` to remove the stacked command
> NOTE: type `_` to recall the stacked command 
> NOTE: type `.unstick` to undo stick-to-top-prompt


# project scope:

* wrappers 
* small composable functions
* add completion to popupar tools (like curl)
* offline utilities  (with markdown as exception)
* make use of installed devlangs (python/perl/awk)
* bash golf 
* bash equalivent of lodash/underscore with interactive convenience

