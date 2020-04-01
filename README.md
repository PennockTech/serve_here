serve_here
==========

These are some Python or Shell scripts for using Python's simple HTTP server
class to serve some files.

## Commands

### `serve_here`

This eponymous script is a shell wrapper which tries Python 3, then Python 2,
to simply invoke the stdlib HTTP server logic to serve the current directory.

As Python 2 falls away, the advantage of this over
`python -m http.server 8000` falls away too.

### `serve_accept_files`

Anonymous insecure file upload, in Python3.

Provides a simple HTML form for allowing browsers to upload file content, and
writes that content out into the current directory.

There is no authentication.  There is minimal security filtering.  It does
not protect against existing file overwrite.  This is not suitable for leaving
running some place.

It is useful for quick and dirty HTTP file upload to your current working
directory.

(Honestly, I forgot I had this until I copied the scripts into this new repo).

### `serve_here_more`

A Python3 script to augment the `serve_here` model by subclassing
`http.server.SimpleHTTPRequestHandler` to add functionality.  This is my
day-to-day workhorse for when I want to expose files in my current directory
to the local network.

* Advertises via Zeroconf if appropriate libraries are installed, so that the
  web-server appears in local-network lists in various mobile/tablet
  applications
* Better directory index listing which is compatible with mobile clients
* Reports URLs at start-up so you can see what clients should be pointed at
* Adds more MIME files to places to look
* Hard-codes a few MIME types
  + primarily for `application/x-openvpn-profile` and `application/wasm`
* If a requested file is missing, will look for compressed variants and serve
  them up with the MIME type as though it were found at the original filename,
  but with `Content-Encoding` applied.
  + Useful after `zopfli main.wasm` to shrink the size of a WASM binary
    served, but keeping all the MIME types correct.

## History

All these are exports from my dot-personal git repository.

* `serve_here` was written in 2014 and has not been changed since.  It just
   works.
* `serve_accept_files` was written in Feb 2017 and the only changes have been
   stylistic.
* `serve_here_more` is my normal workhorse; it was written in Apr 2017 and
   every few months gets various tweaks to make something else work.
