
# Make go restart

A sample project with a Makefile to restart the go-server if the source-code changes. 

# Prerequisites

* Install `inotifywait` with apt
* If on mac, substitute inotifywait with `fswatch`, available via brew.


## Usage

    $ make watch

* Start watching the source-code and restarting the server with the command `make watch`. 
* Stop watching with `ctrl-c`.
* Clean up temporary files with the `clean` target, `make clean`


## How does it work?

When writing a server in go, it is not possible or necessary to do partial reloads of the application during development. A restart of the process is fast enough(sub-second, typically 5-600ms). 

See the [Makefile](Makefile) for how the `make watch` target is working.  


The watch target when using `inotifywatch`
```
watch: clean server.PID
	while true ; do \
		date; \
		make .restartServer ;\
		inotifywait -qre close_write . ; \
	done
```

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
