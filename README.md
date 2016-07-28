# PHP-Server
##### Makes the PHP's built-in web server easier and more practical to use

## Introduction

### Why should you use this tool instead of a "real" web server?

Since version 5.4, PHP provides a built-in web server that can be quite useful as a lighweight and dead-easy-to-install **development web server**.
With it, you do not have to install and configure *Apache*, *NGINX* or any other web server on your machine, just to be able to view local static websites or PHP web sites/applications.

With **PHP-Server**, it becomes even more practical and simpler to use. Also, as explained below, it allows you to browse all your local websites at any time, and you can also make it start automatically when you log in to your computer, making it a complete replacement of a "real" web server, suitable enough for most of your PHP development needs. 

### Features

This command line tool:

1. Provides a set of commands to make it easier to control PHP's built-in web server
2. Runs the server on the background (it doesn't block your terminal, you can even close it)
3. Extends the server's functionality with a custom router that:
    
    1. Auto-generates directory index pages for URLs that match directories having no `index.php` or `index.html` files, allowing you to browse your directory structure in search of sites to open;
     
    2. Supports "virtual URLs" (aka "clean URLs" or "vanity URLs") by automatically redirecting virtual paths to the application's `index.php`, where it can be further routed.

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

> Make sure your `$PATH` environment variable includes `~/.composer/bin`, otherwise the terminal won't be able to find executable files that are installed globally by Composer.

## Usage

Type `php-server` in your terminal, on any directory, to display the list of available commands and their syntax.

```
NAME
    php-server -- makes the PHP's built-in web server easier and more practical to use

SYNTAX
    php-server command [options]
    php-server [--help]

COMMAND
    start - Starts the web server.

        SYNTAX
            php-server start [-p|--port] [-a|--address] [-l|--log] [-g|--global] [-r|--root]

        OPTIONS
            -p, --port     The TCP/IP port the web server will listen on. [default: 8000]
            -a, --address  The IP address the web server will listen on.  [default: localhost]
            -l, --log      The path of a log file where the server's logging output will be saved. [default: /dev/null]
            -g, --global   If specified, the server will serve all sites under the root web directory.
            -r, --root     The root web directory's name or path. If it's a name, the directory will be searched
                           for starting at the current directory and going upwards. Alternatively, you may specify the
                           full path. [default: Sites]

COMMAND
    stop - Stops the web server.

        SYNTAX
            php-server stop

COMMAND
    status - Checks if the web server is running.

        SYNTAX
            php-server status
```

### Local mode

If you run `php-server start`, it will make the current directory available on `http://localhost:8000`. You can use this mode for opening a specific PHP site/application or a static website on a specific HTTP port. You can also launch many sites concurrently on different ports.

### Global mode

If you run `php-server start -g`, it will make available all sites that are installed under a common web folder (it defaults to `~/Sites`, for compatibility with Mac OS X, but you can specify an alternate path).

### Permanent web server

You may configure your operating system to launch `php-server` on global mode on the system's bootup process, after you log in. That way, you'll get a nice replacement for a local *Apache* or *NGINX* that is always ready to server your local websites.

> Instructions on how to auto-start `php-server` on login are beyond the scope of this Readme. Just configure PHP-Server as you would any other auto-starting application; the way to do it depends on your operating system.

### The directory indexes

If you open `http://localhost:8000` on your web browser, you'll see a directory listing of all folders/sites available. From there, you can navigate the directory tree by clicking the folder names, until you reach a folder that has an `index.php` or `index.html` file; in which case the site/application will be lauched.

## Compatibility

PHP-Server is compatible with most PHP websites/applications, even if they seem to require Apache's `mod-rewrite` to run (for instance: most Laravel applications run perfectly). Unless you require advanced web server configuration/functionality, it should work *out-of-the-box*.

## License

This tool is open-source software licensed under the [MIT license](http://opensource.org/licenses/MIT). See the accompanying `LICENSE` file.

Copyright &copy; Cláudio Silva and Impactwave, Lda.
