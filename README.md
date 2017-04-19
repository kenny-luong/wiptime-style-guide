# wiptime-style-guide
Styling Conventions for WIPTime

**Source Code Layout**

*UTF-8 for source file encoding
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

*Don't use <pre><code>;</code></pre> to separate statements and expressions. Use only one expression per line.

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

*No spaces after <pre>(</pre>,<pre><code>[</code></pre>, or before <pre><code>]</code></pre>, <pre><code>)</code></pre>. Use spaces around <pre><code>{</code></pre> and before <pre><code>}</code></pre>

```
# bad

some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# good

some(arg).other
[1, 2, 3].each { |e| puts e }
```

<pre><code>{</code></pre>
