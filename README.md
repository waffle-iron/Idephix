[![Stories in Ready](https://badge.waffle.io/ideatosrl/Idephix.png?label=ready&title=Ready)](https://waffle.io/ideatosrl/Idephix)
Idephix - Automation and Deploy tool
====================================

Idephix is a PHP tool for building automated scripts

[![Gitter](https://badges.gitter.im/ideatosrl/Idephix.svg)](https://gitter.im/ideatosrl/Idephix?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)
[![Build Status](https://travis-ci.org/ideatosrl/Idephix.svg)](https://travis-ci.org/ideatosrl/Idephix)
[![Code Climate](https://codeclimate.com/github/ideatosrl/Idephix/badges/gpa.svg)](https://codeclimate.com/github/ideatosrl/Idephix)
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/47596bd6-4ac9-4314-b79a-1f2e50292c1f/mini.png)](https://insight.sensiolabs.com/projects/47596bd6-4ac9-4314-b79a-1f2e50292c1f)

Installation / Usage
--------------------

1. Download the [`idephix.phar`](http://getidephix.com/idephix.phar) executable.

    ``` sh
    $ curl http://getidephix.com/idephix.phar > idephix.phar
    ```


2. Create a idxfile.php in the root directory of your project. Define your tasks.

    ```php
    <?php
    
    /**
     * Execute the touch of a file specified in input
     * @param string $name the name of the file to be touch-ed
     * @param bool   $go   if not specified the script execute a dry-run
     */
    function testParams($idx, $name, $go = false)
    {
         $idx->local('touch /tmp/'.$name);
         $idx->remote('touch /tmp/'.$name.'_remote');
    }

    $idx->run();

    ```
    
3. Create a idxrc.php in the root directory of your project. The file must return a `Config` Dictionary. 
The returned object will contains all targets info and the SSH client to uso for remote
connections.

    ```php

    $targets = array(
        'prod' => array(
            'hosts' => array('127.0.0.1'),
            'ssh_params' => $sshParams,
            'deploy' => array(
                'local_base_dir' => $localBaseDir,
                'remote_base_dir' => "/var/www/myfantasticserver/",
                // 'rsync_exclude_file' => 'rsync_exclude.txt'
                // 'rsync_include_file' => 'rsync_include.txt'
                // 'migrations' => true
                // 'strategy' => 'Copy'
            ),
        ),
    );
    return \Idephix\Config::fromArray(
        array(
            'targets' => $targets, 
            'sshClient' => new \Idephix\SSH\SshClient(new \Idephix\SSH\CLISshProxy())
        )
    );
    ```

4. Run Idephix: `php idephix.phar --env=test idephix:test-params Nome_file`

Global installation of Idephix
----------------------------------------

You can choose to install idephix wherever you prefer. Idephix use the configuration file in the current path.

1. Go to a PATH directory, e.g. `cd /usr/local/bin`
2. Get Idephix:`curl http://getidephix.com/idephix.phar > idephix.phar`
3. Make the phar executable `chmod a+x idephix.phar`
4. Go to a project directory, e.g. `cd /path/to/my/project`
5. Define your tasks in the idxfile.php file
5. Just invoke the binary `idephix.phar`
6. You can optionally rename the idephix.phar to idx to make it easy to use

Requirements
------------

PHP 5.3.2 or above, >=5.3.12 recommended

Authors
-------

* Manuel 'Kea' Baldssarri <mb@ideato.it>
* Michele 'Orso' Orselli <mo@ideato.it>
* Filippo De Santis <fd@ideato.it>
* [other contributors](https://github.com/ideatosrl/idephix/graphs/contributors)

License
-------

Idephix is licensed under the MIT License - see the LICENSE file for details


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/ideatosrl/idephix/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

