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
