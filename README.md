
# Crystal for Node.js developer

## Contents
<!-- TOC -->

- [Crystal for Node.js developer](#crystal-for-nodejs-developer)
  - [Contents](#contents)
  - [Hello World](#hello-world)
  - [Comments](#comments)
  - [Variables and Constants](#variables-and-constants)
  - [Types](#types)
    - [range](#range)
    - [More about String](#more-about-string)
    - [HEREDOC](#heredoc)
  - [Printing](#printing)
    - [Formatted String](#formatted-string)
      - [Some field type character:](#some-field-type-character)
      - [flags](#flags)
      - [Example:](#example)
    - [Interpolation](#interpolation)
  - [Symbol](#symbol)
  - [Range](#range)
  - [Condition](#condition)
  - [Switch Case](#switch-case)
  - [Iteration](#iteration)
  - [Arrays](#arrays)
  - [Maps](#maps)
  - [Tuple](#tuple)
    - [Typical usage](#typical-usage)
      - [Multiple return value](#multiple-return-value)
      - [Arguments with the splat operator](#arguments-with-the-splat-operator)
    - [Named Tuple](#named-tuple)
      - [Double splat with named tuples](#double-splat-with-named-tuples)
  - [Function](#function)
  - [Callback](#callback)
  - [High Order Function](#high-order-function)
  - [Class](#class)
  - [Struct](#struct)
  - [Enums](#enums)
  - [Module](#module)
  - [Exception](#exception)
  - [Package Manager](#package-manager)
  - [I/O](#io)
  - [Files](#files)
  - [Networks](#networks)
    - [HTTP Server](#http-server)
  - [Encode/Decode](#encodedecode)
    - [JSON](#json)

<!-- /TOC -->

## Hello World

Node.js
```javascript
console.log('Hello World')
```

Crystal

```crystal
puts("Hello World")

puts "Hello World"
```

---

## Comments

Node.js
```javascript
// Single line comment...

/* multi
   Line
   Comment */
```

Crystal

```crystal
# Single line comment

# No
# Multi
# line
# comment
```
---

## Variables and Constants

Node.js
```javascript
var a = 1
const PI = 3.14
let c
```

Crystal

```crystal
a = 1
PI = 3.14

# To declare uninitialized variables
c = uninitialized Int32
```

---

## Types

Node.js
```javascript
let integer_type = 12
let float_type = 1.2
let null_type = null
let bool_type = true
let string_type = 'Dog'
let string_type2 = "Dog"
let multi_line_string = `aa
                         bb
                         cc`
let symbol_type = Symbol('cat')

let object_literal = {
  the_property: "value"
}
let array_type = [1, 2, 3]
let map_type = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
])
let set_type = new Set([1, 2, 3, 4, 5])
```

Crystal

```crystal
integer_type = 12
integer_type2 = 19_i64 # i8, i16, i32, i64, u8, u16, u32, u64
float_type = 1.2
float_type2 = 1.0_f32 # f32, f64
null_type = nil
bool_type = true
char_type = 'Single Quoted'
string_type = "Doule Quoted"
multi_line_string = " All
                     spaces and newlines
                     are preserved "
symbol_type = :cat
array_type = [1, 2, 3] # or %w(one two three)
hash_type = {"one" => 1, "two" => 2}
tuple_type = {1, "hello", 'x'}
named_tuple_type = {one: 1, two: 2}
proc_literal = ->(x : Int32, y : Int32) { x + y }
command_type = `echo foo`  # or %x(echo foo)
```

### range

```crystal
#range

1..5 # inlcude 1 and 5
1...5 # do not include 5
..5
1..
a_range = 1..4
p a_range.to_a # >> [1, 2, 3, 4]
```
### More about String

```crystal
# string in other delimiters
%(hello ("world")) # So you don't have to escape the double quotes in it
%q(hello \n #{name}) # no escape and no interpolation

# string to arrays
%w(foo bar baz) # => ["foo", "bar", "baz"]

# multi-line string without newlines

"hello " \
"world, " \
"no newlines" # => "hello world, no newlines"
```
### HEREDOC

```crystal
# use '<<- identifier' begin, and end in identifier
<<-XML
<parent>
  <child />
</parent>
XML
```

---
## Printing

Node.js
```javascript
console.log('%f The %s %d %o', 0.1, 'answer is', 42, {v: 42})
```

Crystal

```crystal
# all quotation marks might be omitted
puts("hello") # print with newline

p("hello world") # Inspecting print with newline

pp("hello world") # pretty print with newline

print("hello world") # print without newline, then flush output buffer

printf("hello world") # formatting print without newline
```

### Formatted String

The formatted string syntax begin with a '%', end with a field type character, between that are 3 optional part: [flags][width][.precision]

The syntax for a format specifier is:

```
%[flags][width][.precision]field_type_character
```

#### Some field type character:

d: decimal number

f: floating number as [-]ddd.dddddd

c: single character

s: string replaced

%: a literal %

#### flags

space: For numbers, add leading space

+: For numbers, add a leading plus sign

0 (zero): For numbers, pad with zero, other than plus

-: For all, left justify

#### Example:

```
printf("%+d\n", 123)   # +123

printf("%10f\n", 1.2)  # "  1.200000"

printf("%10d\n", 12)   # "        12"

printf("%-3s\n", "hello")  # hello

```

---

### Interpolation

Node.js
```javascript
let key = "Dog"
let value = "Bob"
console.log(`${key} : ${value}`)
```

Crystal

```crystal
key = "Dog"
value = "Bob"
puts "#{key} : #{value}"
puts "%s : %s" % [key, value]
puts "%{key2} : %{value2}" % {key2: "Cat", value2: "Carl"}
```

---
## Symbol

Node.js
```
// No symbol in JS
```

Crystal

A symbol is a **unique** constant that you don't need to give it a value, they can't be created dynamically, the only way to create them is use :(colon), followed by an identifier, the identifier may optionally enclosed in double quotes.

> A double-quoted identifier can contain any unicode character ...

> For an unquoted identifier the same naming rules apply as for methods...

```
:apple
:"cats and dogs" # quoted symbols can include space
:+ # any crystal operator can be a symbol
%i(foo bar baz) # an array of symbols

```
---

## Range

Node.js
```
// No range in JS
```

Crystal

A Range represents an interval between two values. They are usually in parentheses.


- x..y: All values and x, y .
- x...y: All values and x, but NO y.

Both the begin and end are optional.

```
n = [1, 2, 3, 4, 5]
p n[3..]  # => [4, 5], index 3 and all the following
p n.select(3..) # => [3, 4, 5], value equal and greater than 3
```
---

## Condition

Node.js
```javascript
if (true) {
} else if (false) {
} else {
}

true ? true : false
```

Crystal

```crystal
if true
elsif false
else
end

a = true if true

a = if true
      true
    else
      false
    end

a = true ? true : false

unless false
  true
else
  false
end

true unless false

i = true && 5   # i: 5
i = false || 1  # i: 1
i = true || 1   # i: true
```
---

## Switch Case

Node.js
```javascript
let animal = 'Cat'
switch (animal) {
  case 'Dog':
    console.log('Bark')
    break
  case 'Cow':
  case 'Cat':
    console.log('Meow')
    break
  default:
    console.log('Ouch')
}
```

Crystal


```crystal
# no break needed
animal = "Cat"
case animal
when "Dog"
  puts "Bark"
when "Cow"
when "Cat"
  puts "Meow"
else
  puts "Ouch"
end

# Use then to write it in a same  line
animal = "Cat"
case animal
when "Dog" then puts "Bark"
when "Cow" then
when "Cat" then puts "Meow"
else            puts "Ouch"
end

# you can directly invoke methods on expressions as the condition
num = 42
case num
when .even?
  puts "It's even."
when .odd?
  puts "It's odd"
end

# case expression can be omitted
num = 42
case
when num > 10, num < 50
  puts "Greater than 10 OR less than 50"
else
  puts "No"
end
```
---

## Iteration

Node.js
```javascript
// while
while (true) {
  console.log(true)
}

// for
for (let i = 0; i <= 5; i++) {
  console.log(i)
}
```

Crystal

```crystal
# while
while true
  next
  puts true
  break # exit the iteration
end

until false
  puts false
end

# loop
loop do
  puts true
  break
end

def foo
  loop do
    break 'foo' # exit the iteraion, and take 'foo' as the return value of the function
  end
end

```
---

## Arrays

Node.js
```javascript
let foo = []
let a = [1, 2, 3]

a.pop()
a.push(3)
a.shift()
a.unshift(1)

a.splice(3, 0, 4)
a.splice(3, 1, 10)

a.slice(1)
a.slice(1,3)

a.concat([5,6])

a.indexOf(2)

a.forEach(i => console.log(i))

a.map(i => i * 10)
a.filter(i => i > 3)
a.reduce((acc,c) => acc += c, 0)


```

Crystal

```crystal
foo = [] of Int32
foo2 = Array(String).new

a = [1, 2, 3]

a.pop()
a << 4
a.push(4) # alias of <<
a.shift()
a.unshift(1)

a.insert(3, 4) # the inserted will be the index 3

a[1..]    # portion of array: from 1 in end
a[1...3]  # portion of array: from 1 to 3, not include 3
a[1, 3]   # from 1, and size 3
a + [5, 6]  # concat array

a[100]?    # >> nil, to access an element that may not exist
a.includes(32) # >> false
a.delete(2) # delete all value 2.
a.index(3)  # the index of an element

a.each { |i| puts i }

a.map { |i| i + " A." }
a.select { |i| i.size > 3} # same as filter of javascript
a.reduce(0) { |acc, i| acc + i.size }  # use 0 as initial value
```
---

## Maps

Node.js
```javascript
a_map = new Map()
b_map = new Map([['foo', 'foo_value'], ['bar', 'bar_value']])

console.log(b_map.size)

b_map.set('baz', 'baz_value')
b_map.get('baz')
b_map.has('baz')
b_map.delete('baz')

for(let [k, v] of b_map) {
  console.log(k, v)
}

```

Crystal

```crystal
foo = {} of String
foo2 = Hash(String).new
a_map = Hash(String, String).new
a_map["foo"] = "foo_value"
a_map["bar"] = "bar_value"

b_map = { "foo" => "foo_value", "bar" => "bar_value" }
c_map = Hash.zip(["foo", "bar"], ["bar_value", "bar_value"])

puts c_map.size
c_map["quo"]?
c_map.delete("bar")
c_map.has_key?("bar")
c_map.has_value?("bar_value")

a_map.each {|k, v| puts "#{k} : #{v}"}
```
---

## Tuple

Node.js
```javascript
// No tuple in JS
```

Crystal

According to the doc
> A tuple is a fixed-size, immutable, stack-allocated sequence of values of possibly different types.

> You can think of a Tuple as an immutable Array whose types for each position are known at compile time.

```crystal
# Tuples are typically created with literals
a_tuple = Tuple.new
b_tuple = {"foo", 1, 'a'}
c_tuple = Tuple(Int32, Int32).from([1, 2])
b_tuple.size

b_tuple[0] # foo
b_tuple[1] # 1
```

### Typical usage

#### Multiple return value

```
def one_and_cat
  {1, "cat"}
end

one, cat = one_and_cat
p one   # => 1
p cat   # => "cat"
```

#### Arguments with the splat operator

```
# pass tuple as argument list
def multiply(string, value)
  string * value
end

tuple = {"hi", 2}
value = multiply(*tuple)
p value  # "hihi"

# pass arugment list as tuple

def put_in(*args)
  args
end

things = put_in 1, "cat", 'x'
things.class # => Tuple(Int32, String, Char)
p things  # {1, "cat", 'x'}
```


### Named Tuple

Named tuples are like frozen hash.

```
a_named_tuple = {foo: "bar", bar: "baz"}
b_named_tuple = NamedTuple(foo: String, bar: String).from({"foo" => "foo_value", "bar" => "bar_value"})
c_named_tuple = NamedTuple.new
a_named_tuple.size

puts a_named_tuple[:foo]
```

#### Double splat with named tuples

```
def put_in(**args)
  p args # keyword arguments are packed to a named tuple
end

put_in(foo: "foo", bar: "bar")
```
___

## Function

Node.js
```javascript
function add(a, b) {
  return a + b
}
add(1, 2)
```

Crystal

`return` is optional, the last expression will be returned.
Parentheses is optional for function call.
```crystal
def add(a, b)
  a + b #
end

add 1, 2
```
---

## Callback

Node.js
```javascript
function got(data, callback) {
  callback(data)
}
got(12, i => console.log(i))

```

Crystal
All Crystal functions have a hidden block argument you can yield.
```crystal
def got(data)
  yield data
end

got(12) { |i| puts i }
# or
got(12) do |i|
  puts i
end

# if you invoke a method on a single block argument, like...
["a", "b"].join(",") { |s| s.upcase }
# can be rewritten as
["a", "b"].join(",", &.upcase)
```
---

## High Order Function

Node.js
```javascript
function got(data, callback) {
  callback(data)
}
got(12, console.log)
```

Crystal

```crystal
# proc is similar to high order functions or lambda in other languages
log = ->(x : Int32) { puts x }

def got(data)
  yield data
end

# pass the proc as block
got(12, &log)

# You can also pass the proc to the function to capture it, note you
# have to use & in function declaration to declare that the function
# recieves a proc as the argument, and this proc can be returned
# if you want to call it, you need to use Proc method #call.
def got2(&block : Int32 -> Void)
  block
end

proc = got2(&log)
proc.call(22)

# proc can also be created from function
def inc(a)
  a += 1
end

proc = ->inc(Int32)
p proc.call(1)

# a proc is also an object, so it can be created from new method

proc = Proc(Int32, Int32).new { |n, m| n + m }
fn.call(1, 2) # => 3

```

Similar to closure, a proc captures variables.

---

## Class

Node.js
```javascript
class Creature {
  constructor (name) {
    this.name = name
  }
}

const moveMixin = Base => class extends Base {
  move () {
    console.log(`${this.name} moved.`)
  }
}

class Player extends moveMixin(Creature) {
  // #hp  private fields are not currently supported
  constructor (name) {
    super(name)
    this._hp = 999  // convention for private fields
  }

  eat (food) {
    this._hp += food * 10
  }

  get info () {
    return `${this.name}: ${this._hp}`
  }

  set starvation (velocity) {
    this._hp -= velocity * 15
  }

  static register () {
    console.log('You have been registered.')
  }
}

const warrior = new Player('Warrior')
Player.register()               // > "You have been registered."
console.log(warrior.name)       // > "Warrior"
console.log(warrior.info)       // > "Warrior: 999"
warrior.starvation = 0.2
console.log(warrior.info)       // > "Warrior: 996"
warrior.eat(5)                  // > "Warrior: 1046"
console.log(warrior.info)
warrior.move()                  // > "Warrior moved."
```

Crystal

```crystal
class Creature
  property name : String # define setter and getter for name
  def initialize (name : String) # variables that have no initial value need type
    @name = name # instance variables begin with @, they are private by default
  end
end

module Movable # modules can be used as mix-ins
  def move
    puts "#{@name} moved."
  end
end

class Player < Creature
  include Movable
  @@status = "Normal" # class variables begin with @@
  def initialize (name)
    super  # same as super(name)
    @hp = 999.0_F32
  end

  def eat (food : Int32)
    @hp += food * 10
  end

  def info
    "#{@name}: #{@hp}"
  end

  def starvation (velocity : Float32)
    @hp -= (velocity * 15.0).round(0)
  end

  def self.register  # class method begin with self or class name
    puts "You have been registered."
  end

  def self.status
    @@status
  end
end

warrior = Player.new("Warrior")
Player.register()               # > "You have been registered."
puts warrior.name               # > "Warrior"
puts warrior.info               # > "Warrior: 999"
warrior.starvation(0.2)
puts warrior.info               # > "Warrior: 996"
warrior.eat(5)                  # > "Warrior: 1046"
puts warrior.info
warrior.move()                  # > "Warrior moved."
puts Player.status
```
---

## Struct
Node.js
```javascript
// No struct in JS
```

Crystal
Struct is a stack-allocated and pass-by-value type. It is mainly for "immutable data types and/or stateless wrappers of other types".

The syntax is pretty similar to class, just replace 'class' with 'struct'.
```crystal
struct Circle
  def initialize(@x : Int32, @y : Int32, @radius : Int32)
  end

  def area
    3.14 * @radius * @radius
  end

  def enlarge
    @radius += 10
    self
  end
end

c = Circle.new(1,2, 5)
p c.area # 78.5
p c.enlarge.enlarge.area # 1962.5
p c.area # 706.5, note the second enlarge was operated on a copy, which is discarded,
```
---

## Enums

Node.js
```javascript
// no enum in JS
```

Crystal

Enum is a set of integers, each has a name. The integers start with zero and increment by one each time, but can be overwritten. It is recommended that use enums over symbols, especially for public api.
```crystal
enum Season
  Spring
  Summer
  Fall = 10
  Winter

  def snow_ball?
    self == Season::Winter
  end
end

p Season::Spring            # Spring
p Season::Summer.value      # 1
p Season::Fall.value        # 10
p Season::Winter.value      # 11
p Season.new(10)            # Fall
p Season::Fall.snow_ball?   # false
p Season::Winter.snow_ball? # true
```

---

## Module

Node.js
```javascript
// es6
export let foo = 1
export {
  bar
}
export default baz
import { foo, bar } from './foo_and_bar.js'
import baz from './baz.js'

// commonjs
exports.foo = 1
module.exports = {
  bar
}
let { foo } = require('./module_a.js)
let bar = require('./bar.js')
```

Crystal

Crystal use 'require' to import code in other files, it will look up in the two path.
- the standard library location comes with the compiler
- the 'lib' directory relative to the current working directory

```crystal
# could be:
# REQUIRE_PATH/foo.cr
# foo/foo.cr
# foo/src/foo.cr
# foo/src/foo/foo.cr
require "foo"

# could be:
# ./foo.cr
# ./foo/foo.cr
require "./foo"

# The path support nested directories.
# i.e. foo/bar/baz.cr
# or ./foo/bar/baz.cr and so on...
require "foo/bar/baz"
require "./foo/bar/baz"

# Also support wildcards
require "./*"
require "../../foo"
require "../foo/**"
```
---

## Exception

Node.js
```javascript
try {
  throw new Error('oops');
}
catch (ex) {
  console.error(ex);
}
finally {
  console.log('finally');
}

```

Crystal

```crystal
begin
  raise "oops"
rescue ex
  p ex
else
  p "OK"
ensure
  p "finally"
end

# output
# => #<Exception:oops>
# => "finally"

# short syntax

def danger
  raise "oops"
rescue ex
 p ex
end

danger

# short synax also work for block
(1..3).each do |n|
  raise "oops"
rescue ex
p ex
ensure
p 42
end

# output:

# <Exception:oops>
# 42
# <Exception:oops>
# 42
# <Exception:oops>
# 42
```
---

## Package Manager
Node.js
```javascript
npm init
npm install
npm uninstall
npm update
npm run ...
npm test
...
```

Crystal

```crystal
shards init
shards install
shards prune
shards update
shards build
shards list
...
```
---

## I/O
Node.js
```javascript
console.log(process.argv) // [EXECPATH, FILE, ...]
console.log(process.env['MY_ENV']) // MY_ENV=FOOBAR node main.js => FOOBAR
process.stdout.write('output to stdout\n')
process.stderr.write('output to stderr\n')

process.stdin.on('readable', () => {
  let chunk
  while ((chunk = process.stdin.read()) != null) {
    process.stdout.write(`data: ${chunk}`)
  }
})
process.stdin.on('end', () => {
  process.stdout.write('end')
})
```

Crystal

```crystal
puts ENV["MY_ENV"] #  MY_ENV=FOOBAR crystal run hi.cr => FOOBAR
puts ARGV          # crystal run ./src/hi.cr -- foo bar => ["foo", "bar"]
puts gets
STDOUT.puts "output to STDOUT"
STDERR.puts "output to STDERR"
```
----
## Files
Node.js
```javascript
let fs = require('fs')

let fooFile = './foo.txt'
// create
fs.open(fooFile, 'w+', (err, fd) => {
  if (err) {
    console.log(err.message)
    process.exit()
  }
  console.log(`${fooFile} is opened or created.`)
})

// read
fs.readFile(fooFile, 'utf8', (err, data) => {
  if (err) {
    console.log(err.message)
    process.exit()
  }
  console.log(`${fooFile} is opened: `)
  console.log(data)
})

// write
fs.writeFile(fooFile, 'Fantastic content!!!', err => {
  if (err) {
    console.log('Warning: error to write file.')
  }
})

// remove
fs.unlink(fooFile, err => {
  if (err) {
    console.log(err.message)
    process.exit()
  }
  console.log('deleted')
})

```

Crystal

```crystal
fooFile = "./foo.txt"

# create
fd = File.new(fooFile, "w")
fd.close()

# open
fd = File.open(fooFile)
pp fd.gets
fd.close()

# open with block
File.open(fooFile) do |fd|
  pp fd.gets
end

# open and write
File.open(fooFile, "w") do |fd|
  fd.puts "Content 123"
end

# iterate each line
File.each_line(fooFile) do |line|
  pp line
end

# delete file
File.delete(fooFile) if File.exists?(fooFile)

```
---
## Networks
### HTTP Server

Node.js
```javascript
let http = require('http')

let server = http.createServer((req, resp) => {
  resp.writeHead(200, { 'Content-type':'text/plain' })
  resp.write('Hello world!')
  resp.end()
})

server.listen(8998)

```

Crystal

```crystal
require "http/server"

server = HTTP::Server.new do |context|
  context.response.content_type = "text/plain"
  context.response.print "Hello world!"
end

address = server.bind_tcp 8998
puts "Listening on 8998"
server.listen

```
---
## Encode/Decode

### JSON

Node.js
```javascript
let foo = {
  foo: 'foo_value'
}

let jsonStr = JSON.stringify(foo)
let parsedStr = JSON.parse(jsonStr)
```

Crystal

```crystal
require "json"

foo = {
  "foo_key" => "foo_value"
}

jsonStr = foo.to_json
parsedStr = JSON.parse(jsonStr)
```
---
