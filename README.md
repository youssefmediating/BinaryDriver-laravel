# Binary Driver

Binary-Driver is a set of PHP tools to build binary drivers.

[![Build Status](https://travis-ci.org/alchemy-fr/BinaryDriver.png?branch=master)](https://travis-ci.org/alchemy-fr/BinaryDriver)

## AbstractBinary

AbstractBinary provides an abstract class to build a binary driver. It implements
BinaryInterface.

## ProcessBuilderFactory

ProcessBuilderFactory ease spawning processes by generating Symfony [Process]
(http://symfony.com/doc/master/components/process.html) objects.

```php
use Alchemy\BinaryDriver\ProcessBuilderFactory;

$factory = new ProcessBuilderFactory('/usr/bin/php');

// return a Symfony\Component\Process\Process
$process = $factory->create('-v');

// echoes '/usr/bin/php' '-v'
echo $process->getCommandLine();

$process = $factory->create(array('-r', 'echo "Hello !";'));

// echoes '/usr/bin/php' '-r' 'echo "Hello !";'
echo $process->getCommandLine();
```

## Configuration

A simple configuration object, providing an ArrayAccess and IteratorAggregate
interface.

```php
use Alchemy\BinaryDriver\Configuration;

$conf = new Configuration(array('timeout' => 0));

echo $conf->get('timeout');

if ($conf->has('param')) {
    $conf->remove('param');
}

$conf->set('timeout', 20);

$conf->all();
```

Same example using the ArrayAccess interface :

```php
use Alchemy\BinaryDriver\Configuration;

$conf = new Configuration(array('timeout' => 0));

echo $conf['timeout'];

if (isset($conf['param'])) {
    unset($conf['param']);
}

$conf['timeout'] = 20;
```

## License

This project is released under the MIT license.
