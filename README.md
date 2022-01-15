# What is this?

*quickpod* is a tool which can be used to generate ATOM feeds from the files in
a directory. All the metadata included with the feed is derived automatically
so you just need to provide a file listing.

# Usage

```
quickpod [-f|--forever] [-l|--listen IP-OR-HOSTNAME] [-p|--port PORT] FILE [FILE...]
```

- `-f` (`--forever`) is used to make quickpod listen for multiple connections.
  By default it will listen for one connection before exiting.

- `-l` (`--listen`) sets the IP or hostname that quickpod listens on. By default
  it will listen on all network interfaces.

- `-p` (`--port`) sets the port that quickpod listens on. By default it will listen
  on port 8080.
