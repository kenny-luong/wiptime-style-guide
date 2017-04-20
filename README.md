# wiptime-style-guide
Styling Conventions for WIPTime

# Source Code Layout

* UTF-8 for source file encoding
* Two spaces for indentation (soft tabs). *No hard tabs*
```
# bad - four spaces
def some_method
    do_something
end

# good - two spaces
def some_method
  do_something
end
```

* Don't use <code>;</code> to separate statements and expressions. Use only one expression per line.
```
# bad
puts 'foobar'; # unnecessary semicolon

puts 'foo'; puts 'bar' # two expressions on one line

# good
puts 'foobar'

puts 'foo'
puts 'bar'
```

* Prefer a single-line format for class definitions with no body
```
# bad 
class FooError < StandardError
end

# good

FooError = Class.new(StandardError)

or

class FooError < StandardError ; end # this is less okay but preferred over multi-lined class definitions with no body
```

* Avoid single-line methods
```
# bad 

def method_name; body; end

# good

def method_name
  body
end

# an exception would be empty-body methods

def method_name; end
```

* Use spaces around operators, after commas, colons, and semicolons. Proper use of whitespace is key to readability.
```
sum = 1 + 2
a, b = 1, 2
class FooError < StandardError; end
```

* No spaces after <code>(</code>,<code>[</code>, or before <code>]</code>, <code>)</code>. Use spaces around <code>{</code> and before <code>}</code>
```
# bad

some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good

some(arg).other
[1, 2, 3].each { |e| puts e }
```

* In cases where <code>{</code> and <code>}</code> are used for block and hasl literals, as well as string interpolation, the following should be used

* Hash literals*
```
# good - no spaces
{one: 1, two: 2}
```

* Interpolated expressions, there should be no padded-spacing inside the braces*
```
# bad
"From: #{ user.first_name }, #{ user.last_name }"

# good
"From: #{user.first_name}, #{user.last_name}"
```

* No space after <code>!</code>
```
# bad
! something

# good
!something
```

* No space inside range literals
```
# bad
1 .. 3
'a' ... 'z'

# good
1..3
'a'...'z'
```

* Indent <code>when</code> as deep as <code>case</code>
```
# bad
case
  when foo == 'bar'
    puts 'foobar'
  else
    do_nothing
end

# good
case
when foo == 'bar'
  puts 'foobar'
else
  do_nothing
end
```

* When assigning the result of a condition expression to a variable, preserve the usual alignment of its branches
```
# bad
kind = case year
when 1850..1889 then 'Blues'
when 1890..1909 then 'Ragtime'
else 'Jazz'
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# good

kind =
  case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  else 'Jazz'
  end
  
result =
  if some_cond
    calc_something
  else
    calc_something_else
  end
```

* Use empty lines between method definitions and also to break up methods into logical paragraphs internally. It is always recommended to try to keep methods as short as possible. Anything longer than a few lines should be considered for refactoring.
```
# bad

def some_method
  data = initialize(options)
  data.manipulate!
  data.result
end
def some_method
  result
end

# good

def some_method
  data = initialize(options)
  
  data.manipulate!
  
  data.result
end

def some_method
  result
end
```

* Don't use more than one empty line in a row
```
# bad
 some_method
 
 
 
 some_method

# good
  some_method
  
  some_method
```

* Don't use empty lines around method, class, module, or block bodies
```
# bad

class Foo

  def foo
  
    begin
      
      do_something do
        
        something
        
      end
      
    rescue
    
      something
      
    end
    
  end
  
end

# good

class Foo
  def foo
    begin
      do_soemthing do
        something
      end
    rescue
      something
    end
  end
end
```

* Avoid comma after the last paramenter in a method call, especially when the parameters are not on separate lines
```
# bad
some_method(
  size,
  count,
  color,
)

some_method(size, count, color, )

# good
some_method(
  size,
  count,
  color
)

some_method(size, count, color)
```

* Use spaces around the <code>=</code> operator when assigning default values to method parameters:
```
#bad
def some_method(arg1=:default, arg2=nil, arg3=[])
  # do something...
end

# good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
  # do something
end
```

* Avoid line continuation where not required. Avoid using line continuations for anything but string concatenation.
```
# bad
result = 1 - \
         2

# good - but try to avoid
long_string = 'First part of the long string' \
              ' and the second part of the long string'
```

* Use a trailing for multi-line method chaining
```
# bad
one.two.three
  .four

# good
one.two.three.
  four
```

* Align the parameters of a method call if they span more than one line.
```
# bad (double indent)
def send_mail(source)
  Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text)
end

# good
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text
  )
end
```

* Align the elements of the array literals spanning multiple lines.
```
# bad
menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
  'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'].

# good
menu_item =
  ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
   'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
```

* Add underscores to large numeric literals
```
# bad
num = 1000000

# good
num = 1_000_000
```

* Prefer smallcase letters for numeric literal prefixes. <code>0o</code> for octal, <code>0x</code> for hexadecimal, and <code>0b</code> for binary. Do not use <code>0d</code> for decimal literals.
```
# bad
num = 01234
num = 0O1234
num = 0X12AB
num = 0B10101
num = 0D1234
num = 0d1234

# good - easier to separate digits from the prefix
num = 0o1234
num = 0x12AB
num = 0b10101
num = 1234
```

* Limit lines to 80 characters
* Avoid trailing whitespace.
* End each file with a newline.
* Don't use block comments.
```
# bad
=begin
comment
comment
=end

# good
# comment line
# another comment line
```

# Syntax

* Use `::` only to refer nce constants (this includes classes and modules) and constructors (like `Array()` or `Nokogiri::HTML()`). Do not use `::` for regular method invocation.
```
# bad
SomeClass::some_method
some_object::some_method

# good
SomeClass.some_method
some_object.some_method
SomeModule::SomeClass::SOME_CONST
SomeModule::SomeClass()
```

* Use `def` with parentheses when there are parameters. Omit parentheses when the method doesn't accept parameters.
```
# bad
def some_method()
  body
end

# good
def some_method
  body
end

# bad
def some_method_with_parameters param1, param2
  body
end

# good
def some_method_with_parameters(param1, param2)
  body
end
```

* Use parentheses around the arguments of method invocations, especially if the first argument begins with an open parenthesis `(`, as in `f((3 + 2) + 1)`.
```
# bad
x = Math.sin y
# good
x = Math.sin(y)

# bad
array.delete e
# good
array.delete(e)

# bad
temperance = Person.new 'Temperance', 30
# good
temperance = Person.new('Temperance', 30)
```

  Only Omit parentheses for
    - Method calls with no arguments
    ```
    # bad
    Kernel.exit!()
    2.even?()
    fork()
    'test'.upcase()
    
    # good
    Kernel.exit!
    2.even?
    fork
    'test'.upcase
    ```
    
    - Methods that are part of an internal DSL (e.g., Rake, Rails, RSpect):
    ```
    # bad
    validates(:name, presence: true)
    # good
    validates :name, presence: true
    ```
    
    - Methods that have "keyword" status in Ruby:
    ```
    class Person
      # bad
      attr_reader(:name, :age)
      # good
      attr_reader :name, :age
    end
    
    # bad
    puts(temperance.age)
    # good
    puts temperance.age
    ```

* Define optional arguments at the end of the list of arguments. Ruby has some unexpected results when calling methods that have optional arguments at the front of the list
```
# bad
def some_method(a = 1, b = 2, c, d)
  puts "#{a}, #{b}, #{c}, #{d}"
end

some_method('w', 'x') # => '1, 2, w, x'
some_method('w', 'x', 'y') # => 'w, 2, x, y'
some_method('w', 'x', 'y', 'z') # => 'w', x, y, z'

# good
def some_method(c, d, a = 1, b = 2)
  puts "#{a}, #{b}, #{c}, #{d}"
end

some_method('w', 'x') # => '1, 2, w, x'
some_method('w', 'x', 'y') # => 'y, 2, w, x'
some_method('w', 'x', 'y', 'z') # => 'y, z, w, x'
```

* Avoid the use of parallel assignment for defining variables. Parallel assignment is allowed when it is the return of a method call, used with the splat operator, or when used to swap variable assignment. Parallel assignment is less readable than separate assignment.
```
# bad
a, b, c, d = 'foo', 'bar', 'baz', 'foobar'

# good
a = 'foo'
b = 'bar'
c = 'baz'
d = 'foobar'

# good - exception, swapping variable assignment
a = 'foo'
b = 'bar'

a, b = b, a
puts a # => 'bar'
puts a # => 'foo'

# good - method return
def multi_return
  [1,2]
end

first, second = multi_return

# good - use with splat
first, *list = [1, 2, 3, 4] # first => 1, list => [2, 3, 4]

hello_array = *'Hello' # => ["Hello"]

a = *(1..3) # => [1, 2, 3]
```

* Do not use `for`, unless you know exactly why. Most of the time, iterators should be used instead. `for` is implemented in terms of `each` (using `for` will add a level of indirection), but with a twist - `for` doesn't introduce a new scope (unlike `each`) and variables defined in its block will be visible outside of it
```
arr = [1, 2, 3]

# bad
for elem in arr do
  puts elem
end

elem # => 3

# good

arr.each { |elem| puts elem }

elem # => NameError: undefined or local variable or method 'elem'
```

* Do not use `then` for multi-line `if`/`unless`.
```
# bad
if some_condition then
  # body omitted
end

# good
if some_condition
 # body omitted
end
```

* Always put the condition on the same line as the `if`/`unless` in a multi-line conditional.
```
# bad
if
  some_condition
  do_something
  do_something_else
end

# good
if some_condition
  do_something
  do_something_else
end
```

* Favor the ternary operator(`?:`) over the if/then/else/end constructs. It's more common and more concise.
```
# bad
result = if some_condition then something else something_else end

# good
result = some_condition ? something : something_else
```

* Use one expression per branch in a ternary operator. This also means that ternary operators must not be nested. Prefer `if/else` constructs in these cases.
```
# bad
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# good
if some_condition
  nest_condition ? nested_something : nested_something_else
else
  something_else
end
```

* Do not use `if x; ...`. Use the ternary operator instead.
```
# bad
result = if some_condition; something else something_else end

# good
result = some_condition ? something : something_else
```

* Leverage the fact that `if` and `case` are expressions which return a result.
```
# bad
if condition
  result = x
else
  result = y
end

# good
result = 
  if condition
    x
  else
    y
  end
```

* Use `when x then ...` for one-line cases.
* Do not use `when x; ...` as it has been removed as of Ruby 1.9
* Use `!` instead of `not`.
```
# bad - parentheses are required because of op precedence
x = (not something)

# good
x = !something
```

* Avoid the use of `!!`

  `!!` converts a value to a boolean, but you don't need this explicit conversion in the condition of a control expression; using it only obscures your interntion. If you want to do a `nil` check, use `nil?` instead.
  
```
# bad
x = 'test'
# obscure nil check
if !!x
  # body omitted
end

# good
x = 'test'
if x
  # body omitted
end
```

* Do not use `and` and `or`. For boolean expressions, always use `&&` and `||` instead. For flow control, use `if` and `unless`.
```
# bad - boolean expression
ok = got_needed_arguments and arguments_are_valid

# bad - control flow
document.save or fail(RuntimeError, "Failed to save document!")

# good - boolean expression
ok = got_needed_arguments && arguments are valid

# good - control flow
fail(RuntimeError, "Failed to save document!") unless document.save
```

* Favor the modifier `if`/`unless` usage when you have a single-line body. Another good alternative is the usage of control flow `&&`/`||`
```
# bad
if some_condition
  do_something
end

# good
do_something if some_condition
```

* Avoid modifier `if`/`unless` usage at the end of a non-trivial multi-line block.
```
# bad
10.times do
  multi-line body omitted
end if some_condition

# good
if some_condition
  10.times do
    # multi-line body omitted
  end
end
```

* Avoid nested modified `if`/`unless`/`while`/`until` usage. Favor `&&`/`||` if appropriate.
```
# bad
  do_something if other_condition if some_condition

# good
  do_something if some_condition && other_condition
```

* Favor `unless` over `if` for negative conditions.
```
# bad
do_something if !some_condition

# bad
do_something if not some_condition

# good
do_something unless some_condition
```

* Do not use `unless` with `else`. Rewrite these with positive case first.
```
# bad
unless success?
  puts 'failure'
else
  puts 'success'
end

# good
if success?
  puts 'success'
else
  puts 'failure'
end
```

* Don't use parentheses around the condition of a control expression.
```
# bad
if (x > 10) 
 # body omitted
end

# good
if x > 10
  # body omitted
end
```

* Do not use `while/until condition do` for multi-line `while/until`.
```
# bad
while x > 5 do
  # body omitted
end

until x > 5 do
  # body omitted
end

# good
while x > 5
  # body omitted
end

until x > 5
  # body omitted
end
```

* Favor modifier `while/until` usage when you have single-line body
```
# bad
while some_condition
  do_something
end

# good
do_something while some_condition
```

* Favor `until` over `while` for negative conditions.
```
# bad
do_something while !some_condition

# good
do_something until some_condition
```

* Use `loop` instead of `while/until` when you need an infinite loop
```
# bad
while true
  do_something
end

until false
  do_something
end

# good
loop do
  do_something
end
```

* Use `loop` with `break` rather than `begin/end/until` or `begin/end/while` for post-loop tests.
```
# bad
begin
  puts val
  val += 1
end while val < 0

# good
loop do
  puts val
  val += 1
  break unless val < 0
end
```

* Omit the outer braces around an implicit options hash.
```
# bad
user.set({ name: 'John', age: 45, permissions: { read: true } })

# good
user.set(name: 'John', age:45, permissions: { read: true })
```

* Omit both the outer braces and parentheses for methods that are part of an internal DSL.
```
class Person < ActiveRecord::Base
  # bad
  validates(:name, { presence: true, length: { within: 1..10 } })
  
  # good
  validates :name, presence: true, length: { within: 1..10 }
end
```

* Use the proc invocation shorthand when the invoked method is the only operation of a block
```
# bad
names.map { |name| name.upcase }

# good
names.map(&:upcase)
```

* Prefer `{...}` `do...end` for single-line blocks. Avoid using `{...}` for multi-line blocks. Always use `do...end` for "control flow" and "method definitions" (e.g. in Rakefiles and certain DSLs). Avoid `do...end` when chaining.
```
names = %w[Barry Steve Sarah]

# bad
names.each do |name|
  puts name
end

# good
names.each { |name| puts name }

# bad
names.select do |name|
  names.start_with?('S')
end.map { |name| name.upcase }

# good
names.select { |name| name.start_with?('S') }.map(&:upcase)
```

* Avoid `return` where not required for flow of control.
```
# bad
def some_method(some_arr)
  return some_arr.size
end

# good
def some_method(some_arr)
  some_arr.size
end
```

* Use shorthand self assignment operators whenever applicable
```
# bad
x = x + y
x = x * y
x = x**y
x = x / y
x = x || y
x = x && y

# good
x += y
x *= y
x **= y
x /= y
x ||= y
x &&= y
```

* Use `||=` to initialize variables only if they're not already initialized
```
# bad
name = name ? name : 'Your Name'

# bad
name = 'Your Name' unless name

# good - set name to 'Your Name', only if it's nil or false
name ||= 'Your Name'
```

* Don't use `||=` to initialize boolean variables
```
# bad - would set 'enabled' to true even if it was false
enabled ||= true

# good
enabled = true if enabled.nil?
```

* Use `&&=` to preprocess variables that may or may not exist. Using `&&=` wil change the value only if it exists, removing the need to check its existence with `if`
```
# bad
if something
  something = something.downcase
end

# bad
something = something ? something.downcase : nil

# good
something &&= something.downcase
```

* Avoid explicit use of the case equality operator `===`. As its name implies, it is meant to be used implicity by `case` expressions and outside of them it yields some confusing code.
```
# bad
Array === something
(1..100) === 7
/something/ === some_string

# good
something.is_a?(Array)
(1..100).include?(7)
some_string =~ /something/
```

* Do not use `eql?` when using `==` will do. `eql?` is rarely needed.
```
# bad - eql? is the same as == for strings
'ruby'.eql? some_str

# good
'ruby' == some_str
1.0.eql? x # eql? makes ssense here if you want to differentiate between an integer and a float
```

* Do not put a space between a method name and the opening parenthesis
```
# bad
f (3 + 2) + 1

# good
f(3 + 2) + 1
```

* Do not use nested method definitions
```
# bad
def foo(x)
  def bar(y)
    # body omitted
  end
end

# good
def bar(y)
  # body omitted
end

def foo(x)
  bar(x)
end
```

* Prefix with `_` unused block parameters and local variables.
```
# bad
result = hash.map { |k, v| v + 1 }

def something(x)
  unused_var, used_var = something_else(x)
end

# good
result = hash.map { |_k, v| v + 1 }

def something(x)
  _unused_var, used_var = something_else(x)
end
```

* Use `$stdout/$stderr/$stdin` instead of `STDOUT/STDERR/STDIN`. `STDOUT/STDERR/STDIN` are constants.

* Use `warn` instead of `$stderr.puts`. `warn` allows you to suppress warnings if you need to (by setting the warn level to 0 via `-W0`

* When using named format string tokens, favor `%<name>s` over `%{name}` because it encodes information about the type of the value
```
# bad
format('Hello, %{name}', name: 'John')

# good
format('Hello, %<name>s', name: 'John')
```

* Use `Array#join` over `Array#*` with a string argument
```
# bad
%w[one two three] * ', '
# => 'one, two, three'

# good
%w[one two three].join(', ')
# => 'one, two, three'
```

* Use `Array()` instead of explicit `Array` check or `[*var]`, when dealing with a variable you want to treat as an Array, but you're not certain it's an array.
```
# bad
paths = [paths] unless paths.is_a? Array
paths.each { |path| do_something(path) }

# bad (this always creates a new Array instance
[*paths].each { |path| do_something(path) }

# good
Array(paths).each { |path| do_something(path) }
```

* Use `Comparable#between?` instead of complex comparison logic when possible
```
# bad
do_something if x >= 1000 && x <= 2000

# good
do_something if x.between?(1000, 2000)
```

* Use predicate methods to perform explicit comparisons. Numeric comparisons are also OK.
```
# bad
if x % 2 == 0
end

if x % 2 == 1
end

if x == nil
end

# good
if x.even?
end

if x.odd?
end

if x.nil?
end

if x.zero?
end

if x == 0
end
```

* Don't do explicit non-`nil` checks unless you're dealing with boolean values.
```
# bad
do_something if !something.nil?
do_something if something != nil

# good
do_something if something

def value_set?
  !@some_boolean.nil?
end
```

* Avoid the use of `BEGIN` blocks.

* Do not use `END` blocks. Use `Kernel#at_exit` instead.
```
# bad
END { puts 'Goodbye!' }

# good
at_exit { puts 'Goodbye!' }
```

* Avoid the use of nested conditionals for flow of control.

  Prefer a guard clause when you can assert invalid data. A guard clause is a conditional statement at the top of a function that baisl out as soon as it can.
```
# bad
def compute_thing(thing)
  if thing[:foo]
    update_with_bar(thing[:foo])
    if thing[:foo][:bar]
      partial_compute(thing)
    else
      re_compute(thing)
    end
  end
end

# good
def compute_thing(thing)
  return unless thing[:foo] # guard clause
  update_with_bar(thing[:foo])
  return re_compute(thing) unless thing[:foo][:bar]
  partial_compute(thing)
end
```

  Prefer `next` in loops instead of conditional blocks
  ```
  # bad
  [0, 1, 2, 3].each do |item|
    if item > 1
      puts item
    end
  end
  
  # good
  [0, 1, 2, 3].each do |item|
    next unless item > 1
    puts item
  end
  ```

* Prefer `reverse_each` to `reverse.each` because some classes that `include Enumerable` will provide an efficient implementation. Even in the worst case where a class does not provide a specialized implementation, the general implementation inherited from `Enumberable` will be at least as efficient as using `reverse.each`
```
# bad
array.reverse.each { ... }

# good
array.reverse_each { ... }
```

# Naming

* Name identifiers in English

* Use `snake_case` for symbols, methods and variables.
```
# bad
:'some symbol'
:SomeSymbol
:someSymbol

someVar = 5
var_10  = 10

def someMethod
end

def SomeMethod
end

# good
:some_symbol

some_var = 5
var10    = 10

def some_method
end
```

* Do not separate numbers from letters on symbols, methods and variables
```
# bad
:some_sym_1

some_var_1 = 1

def some_method_1
end

# good
:some_sym1

some_var1 = 1

def some_method1
end
```

* Use `CamelCase` for classes and modules. (Keep acronyms like HTTP, RFC, XML uppercase.)
```
# bad
class Someclass
end

class Some_Class
end

class SomeXml
end

class XmlSomething
end

# good
class SomeClass
end

class SomeXML
end

class XMLSomething
end
```

* Use `snake_case` for naming files, e.g. `hello_world.rb`

* Use `snake_case` for naming directories, e.g. `lib/hello_world/hello_world.rb`

* Aim to have a single class/module per source file. Name the file name as the class/module, but replacing CamelCase with snake_case

* Use `SCREAMING_SNAKE_CASE` for other constants
```
# bad
SomeConst = 5

# good
SOME_CONST = 5
```

* Names of methods that return a boolean value should end in a question mark (i.e. `Array#empty?`). Methods that don't return a boolean, shouldn't end in a question mark.

* Avoid prefixing predicate methods with the auxillary verbs such as `is`, `does`, or `can`. These words are redundant and inconsistent with the style of boolean methods in Ruby's core library such as `empty?` and `include?`
```
# bad
class Person
  def is_tall?
    true
  end
  
  def can_play_basketball?
    false
  end
  
  def does_like_candy?
    true
  end
end

# good
class Person
  def tall?
    true
  end
  
  def basketball_player?
    false
  end
  
  def likes_candy?
    true
  end
end
```

* The names of potentiallity dangerous methods (i.e. methods that modify `self` or the arguments, `exit!` (doesn't run the finalizers like exit does, etc) should end with an exclamation mark if there exists a safe version of that dangerous method.
```
# bad - there is no matching 'safe' method
class Person
  def update!
  end
end

# good
class Person
  def update
  end
end

# good
class Person
  def update!
  end
  
  def update
  end
end
```

# Comments

* Write self-documenting code
* Write comments in English
* Use one space between the leading `#` character of the comment and the text of the comment
* Comments longer than a word are capitalized and use punctiation. Use once space after periods.
* Avoid superfluous comments.
```
# bad
counter += 1 # Increments counter by one.
```

* Keep existing comments up-to-date. An outdated comment is worse than no comment at all.
* Avoid writing comments to explain bad code. Refactor the code to make it self-explanatory.

# Comment Annotations

* Annotations should usually be written on the line immediately above the relevant code
* The annotation keyboard is followed by a colon and a space, then a note describing the problem.
* If multiple lines are required to describe the problem, subsequent lines should be indented three spaces after the `#`.
```
def bar
  # FIXME: This has crashed occasionally since v3.2.1. IT may
  #    be related to the BarBazUtilupgrade.
  baz(:quux)
end
```

* In cases where the problem is so obvious that any documentation would be redundant, annotations may be left at the end of the offending line with no note. This usage should be the exception and not the rule.
```
def bar
  sleep 100 # OPTIMIZE
end
```

* Use `TODO` to note missing features or functionality that should be added at a later date.
* Use `FIXME` to note broken code that needs to be fixed.
* Use `OPTIMIZE` to note slow or inefficient code that may cause performance problems.
* Use `HACK` to note code smells where questionable coding practices were used and should be refactored.
* Use `REVIEW` to note anything that should be looked at to confirm it is working as intended. For example, `REVIEW: Are we sure this is how the client does X correctly?`
* If other custom annotation keywords are necessary, be sure to document them.

# Magic Comments

* Place magic comments above all code and documentation. Magic comments should only go below shebangs if they are needed in your source file.
```
# bad
# Some documentation about Person
# frozen_string_literal: true
class Person
end

# good
# frozen_string_literal: true
# Some documentation about Person
class Person
end
```

* Use one magic comment per line if you need multiple.
```
# bad
# -*- frozen_string_literal: true; encoding: ascii-8bit -*-

# good
# frozen_string_literal: true
# encoding: ascii-8bit
```

# Classes & Modules

* Use a consistent structure in your class definitions.
```
class Person
  # extend and include go first
  extend SomeModule
  include AnotherModule
  
  # inner classes
  CustomError = Class.new(StandardError)
  
  # constants are next
  SOME_CONSTANT = 20
  
  #attribute macros
  attr_reader :name
  
  # followed by other macros
  validates :name
  
  #public class methods, next
  def self.some_method
  end
  
  # initialization goes between class methods and other instance methods
  def initialize
  end
  
  # followed by other public instance methods
  def some_method
  end
  
  # protected and private methods are grouped near the end
  protected
  
  def some_protected_method
  end
  
  private
  
  def some_private_method
  end
end
```

* Split multiple mixins into separate statements.
```
# bad
class Person
  include Foo, Bar
end

# good
class Person
  # multiple mixins go with separate statements
  include Foo
  include Bar
end
```

* Don't next multi-line classes within classes. Try to have nested classes each in their own file in a folder named like the containing class.
```
# bad

# foo.rb
class Foo
  class Bar
    # methods
  end
  
  class Car
    # methods
  end
  
  # methods
end

# good

# foo.rb
class Foo
  # methods
end

# foo/bar.rb
class Foo
  class Bar
    # methods
  end
end

# foo/car.rb
class Foo
  class Car
    # methods
  end
end
```

* Prefer modules to classes with only class methods. Classes should be used only when it makes sense to create instances out of them.
```
# bad
class SomeClass
  def self.some_method
    # body
  end
  
  def self.some_other_method
    # body
  end
end

# good
module SomeModule
  module_function
  
  def some_method
    # body
  end
  
  def some_other_method
    # body
  end
end
```

* Favor the use of `module_function` over `extend self` wheny ou want to turn a module's instance methods into class methods.
```
# bad
module Utilities
  extend self
  
  def parse_something(string)
  end
  
  def other_utility_method(number, string)
  end
end

# good
module Utilities
  module_function
  
  def parse_something(string)
  end
  
  def other_utility_method(number, string)
  end
end
```

  `module_function` vs `extend self`:
  
  `module_function` makes the given instance methods private, then duplicates and puts them into the module's metaclass as public methods. `extend self`adds all instance methods to the module's singleton, leaving their visibilities unchanged. 
  
  ```
  module M
    extend self

    def a; end

    private
    def b; end
  end

  module N
    def c; end

    private
    def d; end

    module_function :c, :d
  end

  class O
    include M
    include N
  end

  M.a
  M.b  # NoMethodError: private method `b' called for M:Module
  N.c
  N.d
  O.new.a
  O.new.b  # NoMethodError: private method `b' called for O
  O.new.c  # NoMethodError: private method `c' called for O
  O.new.d  # NoMethodError: private method `d' called for O
  ```

* Try to make your classes as SOLID as possible
* Always supply a proper `to_s` method for classes that represent domain objects.
```
class Person
  attr_reader :first_name, :last_name
  
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end
  
  def to_s
    "#{@first_name #{@last_name}"
  end
end
```

* Use the `attr` family of functions to define trivial accessors or mutators
```
# bad
class Person
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name  = last_name
  end
  
  def first_name
    @first_name
  end
  
  def last_name
    @last_name
  end
end

# good
class Person
  attr_reader :first_name, :last_name
  
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name  = last_name
  end
end
```

* For accessors and mutators, avoid prefixing methods name with `get_` and `set_`. It is a Ruby convention to use attribute names for accessors (readers) and `attr_name=` for mutators (writers)
```
# bad
class Person
  def get_name
    "#{@first_name} #{@last_name}"
  end
  
  def set_name(name)
    @first_name, @last_name = name.split(' ')
  end
end

# good
class Person
  def name
    "#{@first_name} #{@last_name}"
  end
  
  def name=(name)
    @first_name, @last_name = name.split(' ')
  end
end
```

# Numbers

* Use `Integer` check type of an integer number. Since `Fixnum` is platform-dependent, checking against it will return different results on 32-bit and 64-bit machines.
```
timestamp = Time.now.to_i

# bad
timestamp.is_a? Fixnum
timestamp.is_a? Bignum

# good
timestamp.is_a? Integer
```

* Prefer to use ranges when generating random numbers instead of integers with offsets, since it clearly states your intentions.
```
# bad
rand(6) + 1

# good
rand(1..6)
```

# Strings

* Prefer string interpolation instead of string concatenation:
```
# bad
email_with_name = user.name + ' <' + user.email + '>'

# good
email_with_name = "#{user.name} <#{user.email>"
```

* Prefer single-quoted strings when you don't need string interpolation or special symbols such as `\t`, `\n`, `'`, etc.

* Don't use the character literal syntax `?x`. Since Ruby 1.9, it's basically redundant - `?x` would be interpreted as `'x'`
```
# bad
char = ?c

# good
char = 'c'
```

* Don't leave out `{}` around instance and global variables being interpolated into a string.
```
class Person
  attr_reader :first_name, :last_name
  
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name  = last_name
  end
  
  # bad
  def to_s
    "#@first_name #@last_name"
  end
  
  # good
  def to_s
    "#{@first_name #{@last_name}"
  end
end

$global = 0
# bad
puts "$global = #$global"

# good
puts "$global = #{$global}"
```

* Don't use `Object#to_s` on interpolated objects. It's invoked on them automatically.
```
# bad
message = "This is the #{result.to_s}."

# good
message = "This is the #{result}."
```

* Avoid using `String#+` when you need to construct large data chunks. Instead, use `String#<<`. Concatenation mutates the string instance in-place and is always faster than `String#+`, which creates new string objects.
```
# bad
html = ''
html += '<h1>Page Title</h1>'

paragraphs.each do |paragraph|
  html += "<p>#{paragraph}</p>"
end

# good and faster
html = ''
html << '<h1>Page Title</h1>'

paragraphs.each do |paragraph|
  html << "<p>#{paragraph}</p>"
end
```

* Don't use `String#gsub` in scenarios in which you can use a faster more specialized alternative.
```
url = 'http://example.com'
str = 'lisp-case-rules'

# bad
url.gsub('http://', 'https://')
str.gsub('-', '_')

# good
url.sub('http://', 'https://')
str.tr('-', '_')
```

# Date &  Time

* Prefer `Time.now` over `Time.new` when retrieving the current system time.
* Don't use `DateTime` unless you need to account for historical calendar reform -- and if you do, explicity specifiy the `start` argument to clearly state your intentions
```
# bad
DateTime.now - uses DateTime for current time

# good - uses Time for current time
Time.now

# bad - uses DateTime for modern date
DateTime.iso8601('2016-06-29')

# good - uses Date for modern date
Date.iso8601('2016-06-29')

# good uses DateTime with start argument for historical date
DateTime.iso8601('1751-04-23', Date::ENGLAND)
```

# Misc

* Write `ruby -w` safe code.
* Avoid hashes as optional parameters. Does the method do too much? (Object initializers are exceptions for this rule).
* Avoid methods longer than 10 LOC (lines of code). Ideally, most methods will be shorter than 5 LOC. Empty lines do not contribute to the relevant LOC.
* Avoid parameter lists longer than three or four parameters.
* If you really need "global" methods, add them to Kernel and make them private
* Use module instance variables instead of global variables
```
# bad
$foo_bar = 1

# good
module Foo
  class << self
    attr_accessor :bar
  end
end

Foo.bar = 1
```

* Code in a functional way, avoiding mutation when that makes sense.
* Do not mutate parameters unless that is the purpose of the method.

  `mutation` is when you have to change an object

* Avoid more than three levels of block nesting.
