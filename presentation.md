class: center, middle
## PHP
## Mostly harmless

---
## Variables / Identifiers

```php
$x = 1; // local var
$thing->x = 1; // instance var
$this->x = 1; // instance var within a class
Thing::$x = 1; // static var on a class
self::$x; // static var within a class
Thing::X; // class const
self::X; // class const within a class
```

---
## Normal Stuff: classes

```php
class Something {
   public function do() {
      // code!
   }
}
```

---
## Normal Stuff: class constructors

```php
class Something {
   private int $id;

   public function __construct(int $id) {
      $this->id = $id;
   }
}
```

---
## Normal Stuff: subclasses

```php
class Something extends SomethingElse {
   public function do() {
      parent::do();
      // more stuff
   }
}
```

---
## Normal Stuff: procedural code

```php
$things = new /Ds/Vector();
$producer = new Producer();
$things->push($producer);
```

---
## Normal Stuff: namespaces

```php
namespace iFixit\Framework;

class Routable { ... }
```

---
## Normal Stuff: use

```php
use iFixit\Framework\Routable;

$r = new Routable();
```

---

## Starting fresh

Each request starts with a clean slate

---

## Primitive Data Types

* int
* float
* string
* boolean
* array - wtf?

---

## By-value vs By-ref

Primitives are by-value, Objects are by-ref

```php
$y = 1;
$x = $y;
$x = 5;  // $y is still 1

$y = new Thing();
$y->id = 1;
$x = $y;
$x->id = 5 // $y->id == 5
```

---

## Arrays are By-value!

```php
$x = [1, 2];
$y = $x;
$y[0] = "new value";
// $x hasn't changed!
```

---

## Type Co-ercion

PHP ignores types unless you tell it not to.

```php
function add(int $x) {
   return $x + 1;
}

add(1); // 2
add("1"); // 2
add("1e1"); // 11
add("1abc"); // 2
```

---

## Equality

Watch out, cross type comparisons
are wacky. Use === where appropriate.

```php
1 == "1" // true
0 == "null" // true
0 == "what?" // true
false == "0" // true
true == "abc" // true
"abc" == 0.0 // true
```

---

## Strict types

Strict type checking enforces that each call made in the file sends the correct types.
Note: int and float are different types, be careful.

```php
<? declare(strict_types=1)

function add(int $x) { return $x + 1; }

add("123") // type error!
```

---

## Weird stuff:static and self

```php
class Other {
   static function do() { }
   static function another() {
      self::do(); // calls the above func
      static::do(); // calls do() in subclass
      // if this class is extended
   }
}
```

---

## Weird stuff: array keys

If an array key is an int, it'll be used as an int

```php
  $x['3'] = 'a';
  $x[3] = 'a'; // equivalent
  // $x === [3 => 'a'];
```

---

## Weird stuff: Array construction

Arrays don't have to be initialized:

```php
  $x[0][2] = 'a';
  // $x === [0 => [2 => 'a']];
```

---

## Array usage

Arrays are a swiss-army knife, but there
are often better tools for the job.

Google: "php-ds"

---

## Weird stuff: $$

Variables can be loaded dynamically. Generally: don't use this.

```php
$x = 123;
$y = 'x';
$$y == $'x' == 123;
```
---

## Weird stuff: Closures

```php
$total = 0;
$inc = function() use ($total) {
   $total++; // does nothing
}
```
