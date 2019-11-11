# PHPUnit Method annotations 

## @dataProvider

Arbitrary arguments are accepted by the test method. 
These arguments are provided by *data provider* method, 
which is a *public* and returns an array of arrays or objects. 

We can specify the data provider method by `@dataProvider` annotation.

```php
<?php

use PHPUnit\Framework\TestCase;
use App\Services\World;

class WorldTest extends TestCase
{
    /**
     * @dataProvider helloProvider
     */
    public function testHello()
    {
        $world = new World();

        $this->assertEquals('Hello Kenny', $world->hello('Kenny'));
    }

    public function helloProvider()
    {
        return [
            ['Kenny', 'Hello Kenny'],
            [null, 'Hello stanger'],
        ];
    }
}
```

## @depends

PHPUnit supports explicit dependencies between test methods. By using @depends annotations, we can ask PHPUnit to start one method after another.

```php
<?php

use PHPUnit\Framework\TestCase;

class DependTest extends TestCase
{
    public function testEmpty()
    {
        $value = [];
        $this->assertEmpty($value);
        return $value;
    }
    
    /**
     * @depends testEmpty
     */
    public function testPush(array $value)
    {
        array_push($value, 'first');
        $this->assertEquals('first', $value[count($value) - 1]);
        $this->assertNotEmpty($value);
        return $value;
    }
}
```

We declare one variable in `testEmpty()` and use the same variable in dependent methods. `testPush()` method depends on `testEmpty()` as the return value can be used in `testPush()` method. 