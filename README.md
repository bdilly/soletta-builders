# Soletta Builders

**THIS CODE IS STILL IN EXPERIMENTAL STAGE AND SHOULDN'T BE USED IN PRODUCTION.**

This project is composed by

 * The `sol` tool which is a client/server software to aid building
   things remotely. For convenience the client and server code is in
   the same program, but this is not necessary. The client talks via
   HTTP to either request a list of builders or to post a new
   build. When posting a build it sends all the files that match

 * The matching includes directories with plat- prefix that the name
   match the platform and directories with tag- prefix that the name
   match the tags passed on the command line.

 * A set of directories in `platform-*` to prepare build environments
   for different platforms. Each directory contains a `prepare` script
   that does all the necessary setup and produces in `out/platform-*` a
   complete build environment with a `compile` script.

   Common functionality for the different platforms are in `common/`.

 * A set of test programs in `tests` that are valid Soletta programs
   that build environments prepared with the tools above. They are
   expected to be compiled using `sol`. It's encouraged to create new
   tests instead of growing one of the tests to the limit, that way its
   easier to check when a builder is not work what might be the issue.

To get things running

 * Compile `sol` tool by calling `go build` inside the `sol` directory.

 * Call platform-\*/prepare for one or more platforms. This will
   generate an `out/` directory with a subdirectory for each platform.

 * Enter the `out/` directory and run `sol -run-as-server`. This will
   run the server process, a lot of debug output will appear here.

 * Go to any of the tests subdirectory and call `sol` to list the
   available platforms, and `sol PLATFORM-NAME` to call it. This will
   generate a zip file in the `out` directory inside the test,
   containing the result image and necessary tools. If the server is
   in a different machine, use `-addr address:port` option.
