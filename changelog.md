Changelog
=========

## v0.5.9 - March 14, 2011

Fix bug with empty Array arguments - Andy Ray

## v0.5.8 - March 14, 2011

Add `MONITOR` command and special monitor command reply parsing.

## v0.5.7 - February 27, 2011

Add magical auth command.

Authentication is now remembered by the client and will be automatically sent to the server
on every connection, including any reconnections.

## v0.5.6 - February 22, 2011

Fix bug in ready check with `return_buffers` set to `true`.

Thanks to Dean Mao and Austin Chau.

## v0.5.5 - February 16, 2011

Add probe for server readiness.

When a Redis server starts up, it might take a while to load the dataset into memory.
During this time, the server will accept connections, but will return errors for all non-INFO
commands.  Now node_redis will send an INFO command whenever it connects to a server.
If the info command indicates that the server is not ready, the client will keep trying until
the server is ready.  Once it is ready, the client will emit a "ready" event as well as the
"connect" event.  The client will queue up all commands sent before the server is ready, just
like it did before.  When the server is ready, all offline/non-ready commands will be replayed.
This should be backward compatible with previous versions.

To disable this ready check behavior, set `options.no_ready_check` when creating the client.

As a side effect of this change, the key/val params from the info command are available as
`client.server_options`.  Further, the version string is decomposed into individual elements
in `client.server_options.versions`.

## v0.5.4 - February 11, 2011

Fix excess memory consumption from Queue backing store.

Thanks to Gustaf Sjöberg.

## v0.5.3 - February 5, 2011

Fix multi/exec error reply callback logic.

Thanks to Stella Laurenzo.

## v0.5.2 - January 18, 2011

Fix bug where unhandled error replies confuse the parser.

## v0.5.1 - January 18, 2011

Fix bug where subscribe commands would not handle redis-server startup error properly.

## v0.5.0 - December 29, 2010

Some bug fixes:

* An important bug fix in reconnection logic.  Previously, reply callbacks would be invoked twice after
  a reconnect.
* Changed error callback argument to be an actual Error object.

New feature:

* Add friendly syntax for HMSET using an object.

## v0.4.1 - December 8, 2010

Remove warning about missing hiredis.  You probably do want it though.

## v0.4.0 - December 5, 2010

Support for multiple response parsers and hiredis C library from Pieter Noordhuis.
Return Strings instead of Buffers by default.
Empty nested mb reply bug fix.

## v0.3.9 - November 30, 2010

Fix parser bug on failed EXECs.

## v0.3.8 - November 10, 2010

Fix for null MULTI response when WATCH condition fails.

## v0.3.7 - November 9, 2010

Add "drain" and "idle" events.

## v0.3.6 - November 3, 2010

Add all known Redis commands from Redis master, even ones that are coming in 2.2 and beyond.

Send a friendlier "error" event message on stream errors like connection refused / reset.

## v0.3.5 - October 21, 2010

A few bug fixes.

* Fixed bug with `nil` multi-bulk reply lengths that showed up with `BLPOP` timeouts.
* Only emit `end` once when connection goes away.
* Fixed bug in `test.js` where driver finished before all tests completed.

## unversioned wasteland

See the git history for what happened before.
