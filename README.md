# What is this?

*quickpod* is a tool which can be used to generate ATOM feeds from the files in
a directory. All the metadata included with the feed is derived automatically
so you just need to provide a file listing.

# Usage

You'll need a CGI server to run quickpod under. The two I'm aware of that allow this are:

- [busybox](https://busybox.net/downloads/BusyBox.html#httpd)
- [Python http.server](https://docs.python.org/3/library/http.server.html)

For example, with Python:

```
mkdir cgi-bin
cp quickpod cgi-bin

QP_DIR="some-directory" python3 -m http.server --cgi
```

This will serve up all the files in `some-directory`.

# Configuration

quickpod is configured using environment variables, which are passed down from
the shell environment through the CGI server.

**QP_DIR** is the directory containing the files to index. If not provided, the
value of the PWD variable is used instead.

**QP_HTTP_BASE** is the prefix that is inserted before each URL in the feed. If
not provided, this is determined using CGI environment variables:

```
http://${SERVER_NAME}:${SERVER_PORT}/
```

Note that some servers (like Busybox httpd) do not set `SERVER_NAME`. For those
you will either need to set `QP_HTTP_BASE`, or set `SERVER_NAME` and let
quickpod generate `QP_HTTP_BASE` using the above format.

**QP_FEED_ID** is the Atom feed identifier, which can be used to serve different
  feeds. By default this the fixed string "urn:quickpod:feed", so without setting
  this variable all readers will recognize all quickpod feeds as the same feed.

# Dependencies

Aside from the previously mentioned CGI-enabled HTTP server, you'll also need a
few other tools:

- A POSIX shell that supports `local` for variable declarations (if you don't
  know, yours probably does)

- POSIX ckutil, basename, date, id
