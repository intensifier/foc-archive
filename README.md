Yet another browser for the <a href='https://futureofcoding.org/community'>Future of Coding Slack</a>
archives, this time as a purely static set of html files.

# Goals

* Self-contained; all you need is some sort of POSIX OS and Lua. No LuaRocks,
  no need to compile additional libraries.

* Offline first. Hosting on the internet is optional; the primary supported
  way to use this data is locally. (Downloading unfortunately requires a lot
  of bandwidth. Reducing bandwidth usage is a work in progress.)

* Git is merely the means of distribution of the data. In particular, don't
  rely on the commit hashes being immutable.

# Steps

* Download and unzip a Slack archive to some directory, say `input/`.

* Generate a list of files inside all channels:
  ```
  ls input/*/*.json > file_list
  ```

* Generate html for `file_list` into directory `output/`:
  ```
  rm -rf output  # clear output
  lua generate_html.lua input/users.json file_list output
  ```

  Tested with Lua 5.1, 5.2, 5.3, 5.4.

  Does _not_ work with filenames with strange characters like spaces, but
  Slack exports seem well-behaved so far.

  Will not perform any operations outside of file operations, and will not
  perform file operations to anything outside of `file_list` and `output/`.

# FAQ

Q: Why did you invent a whole new URL format?

Since this is a statically generated website, I can't use query parameters
containing `?` and `&`.

Q: How do I search?

Use [Github search](https://github.com/akkartik/foc-archive)
