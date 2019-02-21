
# Make go restart

A sample project with a Makefile to restart the go-server if the source-code changes. 

# Prerequisites

* Install `inotifywait` with apt
* If on mac, substitute inotifywait with `fswatch`. See the section "Adjustments for Mac" for details. 

## Usage

    $ make watch

* Start watching the source-code and restarting the server with the command `make watch`. 
* Stop watching with `ctrl-c`.
* Clean up temporary files with the `clean` target, `make clean`


## How does it work?

When writing a server in go, it is not possible or necessary to do partial reloads of the application during development. A restart of the process is fast enough(sub-second, typically 5-600ms). 

The example in the makefile watches for file-changes with the help of `inotifywait`/`fswatch` and takes advantage of `make`s built in support for incremental builds. 

The watch target when using `inotifywatch` is basically a loop that waits until there are file-changes and then triggering a build:
```
watch: clean server.PID
	while true ; do \
		date; \
		make .restartServer ;\
		inotifywait -qre close_write . ; \
	done
```

See the [Makefile](Makefile) for all details.  

# Adjustments for Mac

* Install fswatch , `brew install fswatch`

Change the watch-target to this:

```
watch: clean server.PID
	while true ; do \
		date; \
		make .restartServer ;\
		fswatch *.go -1 ; \
	done
```
