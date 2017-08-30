Google Web Development Best Practices Coding Standard for PHP CodeSniffer
=====================================================
[![Build Status](https://travis-ci.org/jrfnl/Google-WebDev-PHPCS.png?branch=master)](https://travis-ci.org/jrfnl/Google-WebDev-PHPCS)

## Introduction

This is a set of sniffs for [PHP CodeSniffer](http://pear.php.net/PHP_CodeSniffer) which can be used to check for best practices and performance issues with special focus on optimization for Google AMP.


## Installation

### Requirements

* PHP 5.4+.
* [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer): 3.0.2+.

### Installation in a Composer project

* Add the following lines to the `require-dev` section of your `composer.json` file.
    ```json
    "require-dev": {
        "squizlabs/php_codesniffer": "^3.0.2",
        "jrfnl/google-webdev-phpcs": "*"
    }
    ```
* Next, PHP CodeSniffer has to be informed of the location of the standard.
    - If GoogleWebDev is the **_only_** external PHP CodeSniffer standard you use, you can add the following to your `composer.json` file to automatically run the necessary command:
        ```json
        "scripts": {
            "post-install-cmd": "\"vendor/bin/phpcs\" --config-set installed_paths vendor/jrfnl/google-webdev-phpcs",
            "post-update-cmd" : "\"vendor/bin/phpcs\" --config-set installed_paths vendor/jrfnl/google-webdev-phpcs"
        }
        ```
    - Alternatively - and **_strongly recommended_** if you use more than one external PHP CodeSniffer standard - you can use any of the following Composer plugins to handle this for you.

       Just add the Composer plugin you prefer to the `require-dev` section of your `composer.json` file.

       * [DealerDirect/phpcodesniffer-composer-installer](https://github.com/DealerDirect/phpcodesniffer-composer-installer):"^0.4.1"
       * [higidi/composer-phpcodesniffer-standards-plugin](https://github.com/higidi/composer-phpcodesniffer-standards-plugin)
    - As a last alternative in case you use a custom ruleset, _and only if you use PHP CodeSniffer version 2.6.0 or higher_, you can tell PHP CodeSniffer the path to the PHPCompatibility standard by adding the following snippet to your custom ruleset:
        ```xml
        <config name="installed_paths" value="vendor/jrfnl/google-webdev-phpcs" />
        ```
* Run `composer update --lock` to install both PHP CodeSniffer, the GoogleWebDev coding standard and - optionally - the Composer plugin.
* Verify that the GoogleWebDev standard is registered correctly by running `./vendor/bin/phpcs -i` on the command line. GoogleWebDev should be listed as one of the available standards.
* Now you can use the following command to inspect your code:
    ```bash
    ./vendor/bin/phpcs -p . --standard=GoogleWebDev
    ```

### Standalone

1. Install [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) via [your preferred method](https://github.com/squizlabs/PHP_CodeSniffer#installation).

    PHP CodeSniffer offers a variety of installation methods to suit your work-flow: Composer, [PEAR](http://pear.php.net/PHP_CodeSniffer), a Phar file, zipped/tarred release archives or checking the repository out using Git.

    Do ensure that PHP_CodeSniffer's version matches the requirements(#requirements).

    **Pro-tip:** Register the path to PHPCS in your system `$PATH` environment variable to make the `phpcs` command available from anywhere in your file system.

2. Clone the GoogleWebDev standards repository:

        git clone -b master https://github.com/jrfnl/Google-WebDev-PHPCS.git gwdcs

3. Add its path to the PHP_CodeSniffer configuration:

        phpcs --config-set installed_paths /path/to/gwdcs

   **Pro-tip:** Alternatively, you can tell PHP CodeSniffer the path to the GoogleWebDev standard by adding the following snippet to your custom ruleset:
   ```xml
   <config name="installed_paths" value="/path/to/gwdcs" />
   ```

4. Lastly, add the `~/projects/phpcs/bin` directory to your `PATH` environment variable.

You should then see `GoogleWebDev` listed when you run `phpcs -i`.


## Using a custom ruleset

Like with any PHP CodeSniffer standard, you can add GoogleWebDev to a custom PHP CodeSniffer ruleset.

```xml
<?xml version="1.0"?>
<ruleset name="Custom ruleset">
    <description>My rules for PHP CodeSniffer</description>

    <!-- Run against the GoogleWebDev ruleset -->
    <rule ref="GoogleWebDev"/>

    <!-- Run against a second ruleset -->
    <rule ref="PSR2"/>

</ruleset>
```

Other advanced options, such as changing the message type or severity of select sniffs, as described in the [PHPCS Annotated ruleset](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Annotated-ruleset.xml) wiki page are, of course, also supported.


## License

This code is released under the **_TBD_**.
