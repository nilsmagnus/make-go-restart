
# Make go restart

A sample project with a Makefile to restart the go-server if the source-code changes. 

## Usage

    $ make watch

* Start watching the source-code and restarting the server with the command `make watch`. 
* Stop watching with `ctrl-c`.
* Clean up temporary files with the `clean` target, `make clean`


## How does it work?

When writing a server in go, it is not possible or necessary to do partial reloads of the application during development. A restart of the process is fast enough(sub-second, typically 5-600ms). 

See the [Makefile](Makefile) for how the `make watch` target is working.  
