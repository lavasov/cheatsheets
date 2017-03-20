### 7.1

| Example                                               |          Description           |
| ----------------------------------------------------  |:------------------------------:|
|function testReturn(): ?string<br>{<br>&emsp;return null;<br>}<br><br>function test(?string $name)<br>{<br>&emsp;var_dump($name);<br>} | Nullable types |
|function swap(&$left, &$right): void {} | Void functions |
| $data = [<br>&emsp;[1, 'Tom'],<br>&emsp;[2, 'Fred'],<br>];<br><br>[$id1, $name1] = $data[0];<br>foreach ($data as [$id, $name]) | Symmetric array destructuring |
|const PUBLIC_CONST_A = 1;<br>public const PUBLIC_CONST_B = 2;<br>protected const PROTECTED_CONST = 3;<br>private const PRIVATE_CONST = 4; | Class constant visibility |
| function iterator(iterable $iter)<br>{<br>&emsp;foreach ($iter as $val) {}<br>}<br> | iterable pseudo-type <br> may be used in parameter and<br> return types, where it accepts either arrays or objects<br> that implement the Traversable interface.|
|try {<br>} catch (FirstException `|` SecondException $e) {<br>} | Multi catch exception handling |
| $data = [{<br>&emsp; ["id" => 1, "name" => 'Tom'],{<br>&emsp; ["id" => 2, "name" => 'Fred'],<br> ];<br> list("id" => $id1, "name" => $name1) = $data[0];<br> ["id" => $id1, "name" => $name1] = $data[0]; | Support for keys in list(). <br>This enables destructuring of arrays<br> with non-integer or non-sequential keys. |
| var_dump("abcdef"[-2]); // string (1) "e"<br>var_dump(strpos("aabbcc", "b", -3)); // int(3) | Negative string offsets |
| - |Support for AEAD (modes GCM and CCM) in ext/openssl. |
|pcntl_async_signals(true); // turn on async signals<br><br>pcntl_signal(SIGHUP,  function($sig) {<br>&emsp;   echo "SIGHUP\n";<br>});|Asynchronous signal handling|
| - |HTTP/2 server push support in ext/curl|

### 7.0

| Example                                               |          Description           |
| ----------------------------------------------------  |:------------------------------:|
|function sumOfInts(int ...$ints)<br> {<br>&emsp;return array_sum($ints);<br> }|Scalar type declarations: strings (string), integers (int),<br>  floating-point numbers (float), and booleans (bool)<br>  + class names, interfaces, array and callable from php5 |
| function arraysSum(array ...$arrays): array<br> {<br> &emsp;return array_map(function(array $array): int {<br> &emsp;&emsp;return array_sum($array);<br> &emsp;}, $arrays);<br> } |Return type declarations.<br> The same types are available for return type<br> declarations as are available for<br> argument type declarations.|
|$username = $_GET['user'] ?? 'nobody';<br> // This is equivalent to:<br> $username = isset($_GET['user']) ? $_GET['user'] : 'nobody';<br><br>$username = $_GET['user'] ?? $_POST['user'] ?? 'nobody'; | The null coalescing operator (??) has been added<br> as syntactic sugar for the common case<br> of needing to use a ternary in conjunction with isset().<br> It returns its first operand <br>if it exists and is not NULL;<br> otherwise it returns its second operand.|
|echo 1 <=> 1; // 0<br>echo 1 <=> 2; // -1<br>echo 2 <=> 1; // 1 |Spaceship operator|
|$app->setLogger(new class implements Logger {<br> &emsp;public function log(string $msg) {<br> &emsp; &emsp;echo $msg;<br> &emsp;}<br> });<br> |Anonymous classes. These can be used in place<br> of full class definitions for throwaway objects. |
|class A {private $x = 1;}<br>$getX = function() {return $this->x;};<br>echo $getX->call(new A);|Closure::call()|
|$data = unserialize($foo, ["allowed_classes" => ["MyClass", "MyClass2"]]);|Filtered unserialize()|
|use some\namespace\{ClassA, ClassB, ClassC as C};<br> use function some\namespace\{fn_a, fn_b, fn_c};<br> use const some\namespace\{ConstA, ConstB, ConstC};|Group use declarations|
|function gen()<br> {<br> &emsp;yield 1;<br> &emsp;yield 2;<br> &emsp;yield from gen2();<br> }<br><br> function gen2()<br> {<br> &emsp;yield 3;<br> &emsp;yield 4;<br> } | Generators can now delegate to another generator,<br> Traversable object or array|
|var_dump(intdiv(10, 3)); // int(3) |Integer division with intdiv()|
|interface Throwable<br> &emsp;- Exception implements Throwable<br> &emsp;&emsp;- ...<br> &emsp;- Error implements Throwable<br> &emsp;&emsp;- TypeError extends Error<br> &emsp;&emsp;- ParseError extends Error<br> &emsp;&emsp;- AssertionError extends Error<br> |Throwable Interface|

### 5.6

| Example                                               |          Description           |
| ----------------------------------------------------  |:------------------------------:|
| const ARR = ['a', 'b'];  <br> <br> const ONE = 1; <br> const TWO = ONE * 2; <br> | Added constant scalar expressions syntax.<br>https://wiki.php.net/rfc/const_scalar_exprs |
| function f($req, $opt = null, ...$params) { <br>&emsp;//$params is an array containing the remaining arguments. <br>&emsp;printf('$req: %d; $opt: %d; number of params: %d'."\n", <br> &emsp; $req, $opt, count($params)); <br> } | Added dedicated syntax for variadic functions |
|function add($a, $b, $c) {<br>&emsp;return $a + $b + $c;<br>}<br><br>$operators = [2, 3];<br>echo add(1, ...$operators);<br>| Added support for argument unpacking<br> to complement the variadic syntax.<br>https://wiki.php.net/rfc/variadics<br>|
| <br>printf("2 `**` 3 == %d\n", 2 `**` 3); <br>printf("2 `**` 3 `**` 2 == %d\n", 2 `**` 3 `**` 2);<br> $a = 2;<br> $a `**`= 3;<br> printf("a == %d\n", $a); | Added right associative<br> exponentiation operator `(**)`<br>https://wiki.php.net/rfc/pow-operator<br>|
|namespace Name\Space {<br> &emsp;const FOO = 42;<br> &emsp;function f() { echo "test\n"; }<br> }<br><br> namespace {<br> &emsp;use const Name\Space\FOO;<br> &emsp;use function Name\Space\f;<br><br>&emsp;echo FOO."\n";<br> &emsp;f();<br> }<br> | Added use function and use const |

### 5.5

| Example                                               |          Description           |
| ----------------------------------------------------  |:------------------------------:|
|function xrange($start, $limit, $step = 1) {<br>&emsp;for ($i = $start; $i <= $limit; $i += $step) {<br>&emsp;&emsp;yield $i;<br>&emsp;}<br>}<br><br>foreach (xrange(1, 9, 2) as $number) {<br>&emsp;echo "$number ";<br>} | Generators. Support for generators<br>has been added via the yield keyword. |
|try {} catch (Exception $e) {} finally {} | finally keyword added. try-catch blocks now support<br> a finally block for code that should be run<br> regardless of whether an exception has been thrown or not.|
|string password_hash ( string $password , integer $algo [, array $options ] )|New password hashing API|
|$array = [<br>&emsp;[1, 2],<br>&emsp;[3, 4],<br> ];<br><br>foreach ($array as list($a, $b)){<br>&emsp; echo "A: $a; B: $b\n";<br> } |foreach now supports list()|
|echo [1, 2, 3][0]; // 1<br>echo 'PHP'[0]; // P |array and string literal dereferencing|
|namespace Name\Space;<br>class ClassName {}<br><br>echo ClassName::class;//Name\Space\ClassName | Class name resolution via ::class |