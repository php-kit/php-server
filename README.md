# PHP Server
##### An enhanced interface for the PHP's built-in web server

## Introduction

Since version 5.4, PHP provides a built-in web server that can be used for **development purposes**.  
With it, you do not have to install and configure **Apache**, **nginx** or any other web server on your machine, just to be able to view local PHP web sites/applications.

This command line tool:

- provides a set of commands to make it easier to control PHP's built-in web server
- extends the server's functionality with:
    - auto-generated directory index pages for URLs that match directories that have no `index.php` or `index.html` files. 

> **WARNING:** do not use this on a production server, as `php-server` lacks many of the advanced functionality and security other web servers provide.
  >
> Some of the limitations are:
> - it only processes a single request at a time, so it does not scale;
> - it doesn't send cache headers for static files, so caching by the browser is disabled;

## Usage

#### Runtime requirements

- PHP >= 5.4

#### Installation

On the command-line, type:

```sh
composer global require php-kit/php-server
```

> Make sure your `$PATH` environment variable includes `~/.composer/bin`, otherwise the terminal won't be able to find executable files that are installed globally by Composer.

#### Usage

Type `php-server` in your terminal, on any directory, to display the list of available commands and their syntax.

## License

This library is open-source software licensed under the [MIT license](http://opensource.org/licenses/MIT). See the accompanying `LICENSE` file.

Copyright &copy; Cláudio Silva and Impactwave, Lda.
