# PHP-Server
##### A lightweight development web server for running PHP web applications

## Introduction

### Why should you use this tool instead of a "real" web server?

Since version 5.4, PHP provides a built-in web server that can be quite useful as a lighweight and dead-easy-to-install **development web server**.
With it, you do not have to install and configure *Apache*, *NGINX* or any other web server on your machine, just to be able to view local static websites or PHP web sites/applications.

With **PHP-Server**, that embedded server becomes even more practical and simpler to use, making it a suitable replacement of a "real" web server, capable enough for most of your PHP development needs.

### Features

This tool:

1. Is much more lightweight on system resources than a common web server.
0. Is much simpler to install than a web server + PHP integration.
0. Provides a set of commands to make it easier to control PHP's built-in web server.
0. Runs the server on the background by default (it doesn't block your terminal, you can even close it).
0. Can start the server automatically when you log in to your computer.
0. Allows you to browse all your local websites and directories.
0. Extends the server's functionality with:

    1. A custom router that:

        1. Auto-generates directory index pages for URLs that match directories having no `index.php` or `index.html` files, allowing you to browse your directory structure in search of sites to open.

        0. Supports "virtual URLs" (aka "clean URLs" or "vanity URLs") by automatically redirecting virtual paths to the application's `index.php`, where it can be further routed.

    0. Access to your environment variables from PHP scripts

### Limitations

Do not use this on a production server, as `php-server` lacks many of the advanced functionality and security other web servers provide.

Some of the (show-stopper) limitations are:
- It only processes a single request at a time, so it does not scale;
- It doesn't send cache headers for static files, so caching by the browser is disabled;
- It has no support for advanced `mod-rewrite` or `.htaccess` configurations (but see the note above about *virtual URLs*).

## Installation

#### Runtime requirements

- PHP >= 5.4
- [Composer](https://getcomposer.org)
- BASH command line shell

#### Operating system compatibility

- Mac OS X (preferred)
- Linux
- Windows via *Git BASH*, *MSYS2* or *Cygwin*

##### About Windows compatibility

Although this tool is installed via Composer, a big part of it is written in BASH, so you
need BASH to run it.

BASH is not available natively on Windows and **cmd.exe** (the Windows terminal) is not compatible.

One workaround is to install **Git for Windows**, which provides **Git BASH**, and run
this tool with it.

Another way is to install [MSYS2](https://msys2.github.io) or [Cygwin](https://www.cygwin.com);
both provide a port to Windows of many Unix utilities, including BASH.

#### Installation

##### Installing the pre-requisites

First you need to install PHP, if you don't have it yet on your machine.

> For OS X, you can use the amazing PHP installer available at [php-osx.liip.ch](http://php-osx.liip.ch)

To install Composer follow the instructions at [https://getcomposer.org/download]

##### Installing `php-server`
On the command-line, type:

```shell
composer global require php-kit/php-server
```

That's it!

> **Tip:** make sure your `$PATH` environment variable includes `~/.composer/vendor/bin`, otherwise the terminal won't be able to find executable files that are installed globally by Composer, such as this one.

> You may edit your path on `~/.profile`, `~/.bash_profile` or `~/.bashrc`; use the first that exists on your machine.

## Usage

Type `php-server` in your terminal, on any directory, to display the list of available commands and their syntax.

You'll get the following output:

```
NAME
    php-server -- a lightweight development web server for running PHP web applications

SYNTAX
    php-server command [options]
    php-server [--help]

COMMAND
    start - Starts the web server.

        SYNTAX
            php-server start [-p|--port] [-a|--address] [-l|--log] [-n|--no-log] [-g|--global] [-r|--root] [-f|--foreground] [-x|--executable]

        OPTIONS
            -p, --port       The TCP/IP port the web server will listen on.
                             [default: 8000]
            -a, --address    The IP address the web server will listen on.
                             [default: localhost]
            -l, --log        The path of a log file where the server's logging output will be saved.
                             [default: ~/.php-server.log]
            -n, --no-log     Disable logging.
            -g, --global     If specified, the server will serve all sites under the root web directory.
            -r, --root       The root web directory's name or path. If it's a name, the directory will be searched for
                             starting at the current directory and going upwards. Alternatively, you may specify the
                             full path.
                             [default: Sites]
            -f, --foreground Don't run the server as a background process.
            -x, --executable The path to the PHP interpreter.
                             [default: searched on $PATH]

COMMAND
    stop - Stops the web server.

COMMAND
    restart - Stops the web server and starts it again with the same options as before.

COMMAND
    status - Checks if the web server is running.

COMMAND
    install - Installs the server as a system user agent that is auto-started on login.
              The server runs in --global mode.
              This works on macOS only!

        SYNTAX
            php-server install [-p|--port] [-a|--address] [-l|--log] [-n|--no-log] [-r|--root] [-e|--env]

        OPTIONS
            -e, --env        The path to a script that will set environment variables.
                             This is required if you specify a port < 1024, as the server will run from the root user
                             account and it will not inherit the current user's environment.
                             [default: ~/.profile - if the file exists and port < 1024]

COMMAND
    uninstall - Shuts down and uninstalls a previously installed user agent.
                This works on macOS only!

COMMAND
    self-update - Updates this tool to the latest version.
```

### Local mode

If you run `php-server start`, it will make the current directory available on `http://localhost:8000`. You can use this mode for opening a specific PHP site/application or a static website on a specific HTTP port. You can also launch many sites concurrently on different ports.

### Global mode

If you run `php-server start -g`, it will make available all sites that are installed under a common web folder (it defaults to `~/Sites`, for compatibility with Mac OS X, but you can specify an alternate path).

### Permanent web server

You may configure your operating system to launch `php-server` on global mode on the system's bootup process and/or after you log in. That way, you'll get a nice replacement for a local *Apache* or *NGINX* that is always ready to serve your local websites.

On macOS you can use the buit-in command `install` to configure the server to run either as:
- a `daemon` - under the `root` user account, starting on system boot-up, if the HTTP port is < 1024.
- a `user agent` - under the current user account, when he/she logs in, for all other ports.

Use the `uninstall` command to stop the server and prevent it from starting automatically again.

> Currently, there is no built-in support for setting up the server to run automatically on other operating systems.

### The directory indexes

If you open `http://localhost:8000` (using the default php-server configuration) on your web browser, you'll see a directory listing of all folders/sites available. From there, you can navigate the directory tree by clicking the folder names, until you reach a folder that has an `index.php` or `index.html` file; in which case the site/application will be lauched.

## Compatibility

PHP-Server is compatible with most PHP websites/applications, even if they seem to require Apache's `mod-rewrite` to run (for instance: most Laravel applications run perfectly). Unless you require advanced web server configuration/functionality, it should work *out-of-the-box*.

## License

This tool is open-source software licensed under the [MIT license](http://opensource.org/licenses/MIT). See the accompanying `LICENSE` file.

Copyright &copy; Cláudio Silva and Impactwave, Lda.
