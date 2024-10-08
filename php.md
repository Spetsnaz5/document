## 目錄
  - [PHP 7.0](#php-70)
  - [PHP 7.1](#php-71)
  - [PHP 7.2](#php-72)
  - [PHP 7.3](#php-73)
  - [PHP 7.4](#php-74)
  - [PHP 8.0](#php-80)
  - [PHP 8.1](#php-81)
  - [PHP 8.2](#php-82)
  - [PHP 8.3](#php-83)


## 筆記
```
getopt

file_get_contents

array

array_chunk

array_column 

array_diff 差集

array_diff_key

array_filter 

array_flip 交換key value

array_intersect 交集

array_intersect_key

array_keys 回傳所有key

array_values 回傳所有value 

array_map

array_merge

array_shift 拋除頭部

array_unshift 加入頭部

array_pop 拋出末尾

array_push 加入末尾

array_rand 陣列中隨機抽出一個或多個key

array_reverse 回傳順序相反陣列

array_search 搜尋回傳key

array_sum

array_unique 移除重複key

compact

extract

count

in_array

get_class

get_class_vars

get_class_methods

get_object_vars

method_exists

property_exists

__NAMESPACE__

__CLASS__

__METHOD__

__FUNCTION__

```

# PHP 7.0
## Scalar Type Declarations
```php
function addNumbers(int $a, int $b): int {
    return $a + $b;
}

echo addNumbers(5, 10); // 輸出 15
```

## Return Type Declarations
```php
function getName(): string {
    return 'John Doe';
}
```

## Null Coalesce Operator
```php
$name = $_GET['name'] ?? 'Guest';
```

## Spaceship Operator
```php
$result = 1 <=> 2; // 返回 -1
$result = 2 <=> 2; // 返回 0
$result = 3 <=> 2; // 返回 1
```

## Constant Arrays
```php
define('FRUITS', ['apple', 'banana', 'cherry']);
echo FRUITS[1]; // 輸出 'banana'
```

## Anonymous Classes
```php
$object = new class {
    public function greet() {
        return 'Hello, World!';
    }
};

echo $object->greet(); // 輸出 'Hello, World!'
```

## Group Use Declarations
```php
use MyNamespace\{ClassA, ClassB, ClassC as C};
```

## Error Handling Improvements
```php
try {
    // 一些可能導致錯誤的代碼
} catch (\Throwable $e) {
    echo 'Caught: ' . $e->getMessage();
}
```

# PHP 7.1
## Nullable Types
```php
function setAge(?int $age): void {
    // $age 可以是 int 或 null
}

setAge(25);  // 有效
setAge(null); // 也有效
```

## Void Return Type
```php
function sayHello(): void {
    echo "Hello";
    // 沒有 return 語句，或者 return; 也是允許的
}
```

## Class Constant Visibility
```php
class MyClass {
    private const PRIVATE_CONST = 'private';
    protected const PROTECTED_CONST = 'protected';
    public const PUBLIC_CONST = 'public';
}
```

## Multi-catch Exception Handling
```php
try {
    // 可能拋出異常的代碼
} catch (FirstException | SecondException $e) {
    echo "Caught exception: " . get_class($e);
}
```

## Support for Keys in List
```php
$data = [
    ['id' => 1, 'name' => 'John'],
    ['id' => 2, 'name' => 'Jane'],
];

foreach ($data as ['id' => $id, 'name' => $name]) 
    echo "$id: $name \n";
```

```php
$data = [
    [3, 'jack', 'admin'],
    [4, 'tony', 'user'],
];

foreach ($data as [$id, $name, $role]) 
    echo "$id: $name $role \n";
```

```php
$data = [
    ['id' => 1, 'name' => 'John'],
    ['id' => 2, 'name' => 'Jane'],
];

["id" => $id, "name" => $name] = $data[1];

echo "$id $name \n";
```

## Square Bracket Syntax for Array Destructuring
```php
[$a, $b] = [1, 2];
echo $a; // 輸出 1
echo $b; // 輸出 2
```

# PHP 7.2
## Object Type Hinting
```php
function setObject(object $obj): void {
    // 這個函數只能接受對象作為參數
}

setObject(new stdClass()); // 有效
setObject("string"); // 無效，會拋出錯誤
```

# PHP 7.3

## JOIN
```php
try {
    json_decode("{", false, 512, JSON_THROW_ON_ERROR); 
} catch (\JsonException $exception) {
    echo $exception->getMessage(); // echoes "Syntax error" 
}
```

## Trailing Comma in Function Calls
```php
function foo($a, $b, $c) {
    // Some code
}

foo(1, 2, 3,); // 允許尾隨逗號
```

# PHP 7.4
## Typed Properties
```php
class User {
    public int $id;
    public string $name;
}

$user = new User();
$user->id = 1;
$user->name = "John Doe";
```

## Arrow Functions
```php
$numbers = [1, 2, 3, 4];
$squares = array_map(fn($n) => $n ** 2, $numbers);
print_r($squares); // 輸出 [1, 4, 9, 16]
```

## Null Coalescing Assignment Operator
```php
$data['key'] ??= 'default';

#等同以下
if (!isset($data['key'])) {
    $data['key'] = 'default';
}
```

```php
$array = ['name' => 'John'];
$array['name'] ??= 'Doe'; // 會保留 'John'
$array['age'] ??= 30; // 會設置 'age' 為 30
print_r($array); // 輸出 Array ( [name] => John [age] => 30 )
```

## Spread Operator in Array Expression
```php
$array1 = [1, 2, 3];
$array2 = [4, 5, 6];
$combined = [...$array1, ...$array2];
print_r($combined); // 輸出 [1, 2, 3, 4, 5, 6]
```

## Covariant Returns and Contravariant Parameters
```php
class Animal {}
class Dog extends Animal {}

interface Factory {
    function make(): Animal;
}

class DogFactory implements Factory {
    public function make(): Dog { // 協變返回類型
        return new Dog();
    }
}
```

## Numeric Literal Separator
```php
$price = 1_000_000; // 相當於 1000000
```

# PHP 8.0

## JIT
```
```

## Union Types
```php
#int float string bool array object null callable iterable mixed 
function foo(int|float $number): int|float {
    return $number;
}
```

## Named Arguments
```php
function foo($a, $b, $c) {
  echo "{$a}-{$b}-{$c}";
}

foo(a: 1, c: 3, b: 2);
```

## Constructor Property Promotion
```php
class Point {
    public function __construct(
        public float $x = 0.0,
        public float $y = 10.0,
    ) {}
}
```

## Match
```php
$result = match ($status) {
    1 => 'A',
    2 => 'B',
    3 => date("Ymd"),
    4, 5 => "D",
    default => 'Unknown',
};

$age = 23;
$result = match (true) {
    $age >= 65 => 'senior',
    $age >= 25 => 'adult',
    $age >= 18 => 'young adult',
    default => 'kid',
};
```

## Nullsafe
```php
$country = $session?->user?->getAddress()?->country;
```

## Throw Expression
```php
$value = $foo ?? throw new Exception('Invalid value');
```

## ::class
```php

namespace App\Demos;

use Foo\Bar;
use Bar\Baz as BBaz;

class Demo {}

// `use` statement is resolved:
echo Bar::class; // "Foo\Bar"

// `use` X `as` Y is resolved:
echo BBaz::class; // "Bar\Baz"

// Current namespace is resolved:
echo Demo::class; // "App\Demos\Demo"

#在 PHP 8.0 之前，::class物件上不允許使用魔法常數。
$object = new Foo\Bar();
echo $object::class;// "Foo\Bar"
```

# PHP 8.1
## Enumerations
```php
enum Status {
    case Pending;
    case Approved;
    case Rejected;
}

// 使用枚舉
function handleStatus(Status $status): void {
    switch ($status) {
        case Status::Pending:
            // 處理 Pending 狀態
            break;
        case Status::Approved:
            // 處理 Approved 狀態
            break;
        case Status::Rejected:
            // 處理 Rejected 狀態
            break;
    }
}
```

```php
enum UserName: string {
    case ADMIN = 'admin';
    case USER = 'user';
    case GUEST = 'guest';
}

var_dump(UserName::ADMIN->name); // ADMIN
var_dump(UserName::ADMIN->value);// admin
```

## Readonly Properties
```php
class User {
    public readonly string $name;

    public function __construct(string $name) {
        $this->name = $name;
    }
}

$user = new User('John');
echo $user->name; // John
// $user->name = 'Jane'; // 將會拋出錯誤
```

## First-Class Callable Syntax
```php
class MyClass {
    public function sayHello(): void {
        echo 'Hello';
    }
}

$obj = new MyClass();
$callback = $obj->sayHello(...);
$callback(); // 輸出 'Hello'
```

## Fibers
```php
#實現協程（coroutines）和更高效的異步編程
$fiber = new Fiber(function (): void {
    echo "Fiber started\n";
    Fiber::suspend();
    echo "Fiber resumed\n";
});

$fiber->start(); // 輸出 "Fiber started"
$fiber->resume(); // 輸出 "Fiber resumed"
```

## Array Unpacking with String Keys
```php
$array1 = ['foo' => 'bar'];
$array2 = ['baz' => 'qux'];

$result = [...$array1, ...$array2];
print_r($result); // 輸出 Array ( [foo] => bar [baz] => qux )
```

## Intersection Types
```php
interface A {}
interface B {}

function process(A&B $value): void {
    // 處理同時實現 A 和 B 的物件
}
```

## Final 
```php
#防止繼承或覆寫
final class FinalClass {
    public function doSomething(): void {}
}

// 這樣會報錯
// class ExtendedClass extends FinalClass {}
```

# PHP 8.2
## Read-Only Classes
```php
readonly class User {
    public string $name;
    public function __construct(string $name) {
        $this->name = $name;
    }
}
```

## Disjunctive Normal Form (DNF) Types
```php
function example((A&B)|C $input): void {
    // 這裡 $input 可以是 (A&B) 或 C 類型
}
```

## Traits 
```php
trait MyTrait {
    public const MY_CONSTANT = 'value';
}

class MyClass {
    use MyTrait;
}

echo MyClass::MY_CONSTANT; // 輸出 'value'
```

## Dynamic Properties Deprecated
```php
class User {
    public string $name;
}

$user = new User();
$user->name = 'John'; // 正常
$user->age = 30; // 在 PHP 8.2 中觸發棄用警告

## __get __set例外
```

# PHP 8.3
## JSON
```php
$json = '{"name": "John", "age": 30}';
echo json_validate($json) ? 'Valid JSON' : 'Invalid JSON';
```

## Non-local Returns
```php
$callback = function () {
    return 'This is a return value';
};

echo $callback(); // 輸出 'This is a return value'
```

## stdClass
```php
$object = new stdClass();
$object->name = 'John';
$object->age = 30;

$readonlyObject = readonly($object);
// $readonlyObject->name = 'Jane'; // 會引發錯誤，因為物件是只讀的
```

## Dynamic class constant and Enum member
```php
class MyClass {
    public const MY_CONST = 42;
}

$constName = 'MY_CONST';

echo MyClass::{$constName};
```

```php
enum MyEnum: int {
    case MyMember = 42;
}

$enumName = 'MyMember';

echo MyEnum::{$enumName}->value;
```

```php
class Foo {}
$constant = 'class';

echo Foo::{$constant}; // "Foo"
```
