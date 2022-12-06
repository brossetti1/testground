# Example Browser and Node Testplan

With this testplan we want to showcase how one could,
while still using the `docker:generic` builder, have a testplan
which can be tested in a node environment (using `docker:node`)
as well as within a browser. This does require that the library
you wish to test can be used from both environments.

## Usage

Within the root folder of this repository you can run the
integration test for this plan which will run all its test cases
in node and chromium:

```
integration_tests/example_05_browser_node.sh
```

Or in case you want, and already have a `testground daemon` running,
you can also run a single test case as follows:

```
testground run single \
    --plan example-browser-node \
    --testcase output \
    --instances 1 \
    --builder docker:generic \
    --runner local:docker \
    --wait
```

## Remote Debugging

Using the `chrome://inspect` debugger tool,
as documented in <https://developer.chrome.com/docs/devtools/remote-debugging/local-server/>,
you can remotely debug this testplan.

How to do it:

1. start the testplan
2. check what host port is bound to the exposed debug port
3. open `chrome://inspect` in your chrome browser on your host machine
4. configure the network targets to discover: `127.0.0.1:<your port>`
5. attach to the debugger using `inspect`

If you want you can now attach breakpoints to anywhere in the source code,
an a refresh of the page should allow you to break on it.

### Firefox Remote Debugging

Using `about:debugging` you should be able to debug remotely
in a similar fashion. However, for now we had no success
in trying to connect to our firefox instance.

As such you consider Firefox remote debugging a non-supported feature for now,
should you want to remotely debug, please us chromium for now (the default browser).

### WebKit Remote Debugging

No approach for remote debugging a WebKit browser is known by the team.
For now this is not supported.

Please use chromium (the default browser) if you wish to remotely debug.
