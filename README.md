# wiptime-style-guide
Styling Conventions for WIPTime

**Source Code Layout**

* UTF-8 for source file encoding
*Two spaces for indentation (soft tabs). *No hard tabs*
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

*Don't use <code>;</code> to separate statements and expressions. Use only one expression per line.
```
# bad
puts 'foobar'; # unnecessary semicolon

puts 'foo'; puts 'bar' # two expressions on one line

# good
puts 'foobar'

puts 'foo'
puts 'bar'
```

*Prefer a single-line format for class definitions with no body
```
# bad 
class FooError < StandardError
end

# good

FooError = Class.new(StandardError)

or

class FooError < StandardError ; end # this is less okay but preferred over multi-lined class definitions with no body
```

*Avoid single-line methods
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

*Use spaces around operators, after commas, colons, and semicolons. Proper use of whitespace is key to readability.
```
sum = 1 + 2
a, b = 1, 2
class FooError < StandardError; end
```

*No spaces after <code>(</code>,<code>[</code>, or before <code>]</code>, <code>)</code>. Use spaces around <code>{</code> and before <code>}</code>
```
# bad

some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good

some(arg).other
[1, 2, 3].each { |e| puts e }
```

*In cases where <code>{</code> and <code>}</code> are used for block and hasl literals, as well as string interpolation, the following should be used

*Hash literals*
```
# good - no spaces
{one: 1, two: 2}
```

*Interpolated expressions, there should be no padded-spacing inside the braces*
```
# bad
"From: #{ user.first_name }, #{ user.last_name }"

# good
"From: #{user.first_name}, #{user.last_name}"
```

*No space after <code>!</code>
```
# bad
! something

# good
!something
```

*No space inside range literals
```
# bad
1 .. 3
'a' ... 'z'

# good
1..3
'a'...'z'
```

*Indent <code>when</code> as deep as <code>case</code>
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

*When assigning the result of a condition expression to a variable, preserve the usual alignment of its branches
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

*Use empty lines between method definitions and also to break up methods into logical paragraphs internally. It is always recommended to try to keep methods as short as possible. Anything longer than a few lines should be considered for refactoring.
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

*Don't use more than one empty line in a row
```
# bad
 some_method
 
 
 
 some_method

# good
  some_method
  
  some_method
```

*Don't use empty lines around method, class, module, or block bodies
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

*Avoid comma after the last paramenter in a method call, especially when the parameters are not on separate lines
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

*Use spaces around the <code>=</code> operator when assigning default values to method parameters:
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

*Avoid line continuation where not required. Avoid using line continuations for anything but string concatenation.
```
# bad
result = 1 - \
         2

# good - but try to avoid
long_string = 'First part of the long string' \
              ' and the second part of the long string'
```

*Use a trailing for multi-line method chaining
```
# bad
one.two.three
  .four

# good
one.two.three.
  four
```

*Align the parameters of a method call if they span more than one line.
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

*Align the elements of the array literals spanning multiple lines.
```
# bad
menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
  'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'].

# good
menu_item =
  ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
   'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
```

*Add underscores to large numeric literals
```
# bad
num = 1000000

# good
num = 1_000_000
```

*Prefer smallcase letters for numeric literal prefixes. <code>0o</code> for octal, <code>0x</code> for hexadecimal, and <code>0b</code> for binary. Do not use <code>0d</code> for decimal literals.
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

*Limit lines to 80 characters
*Avoid trailing whitespace.
*End each file with a newline.
*Don't use block comments.
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

