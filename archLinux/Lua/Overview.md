# Comments 
```Lua
-- single line 
--[[
	Multi
	Line 
--]]
```

# Variables

### Numbers 
numbers may be integers or floats
```Lua
num = 42
num = 15.5
```

### Strings 
strings are immutable like in python 
```Lua
s = 'testicles' -- single line
t = "whats popin" -- double qoutes work too 
u =[[double 
	bracket
	multi
	line]] -- multiline string 

-- string concatenation 

```

### bools 
`true`
`false` 
*note: only nil and false values are falsy; 0 and '' (empty string) are true!!!*

### nil
the `nil` operator undefines a variable and frees space with Lua's garbage collector 

*note: undefined variables return nil*

# Conditionals 
### Comparison Operators 
`~=` - does not equal
`==` - equals 

```Lua
-- If statements 
if val > 1914 then 
	print('over 1914')

-- elseif statements 
elseif s ~= 21 then
	io.write('cant drink sorry') -- defaults to std. io 

else 
	moonIsCheese = true 
```

# Loops

### While 
```Lua
while num < 100 do 
	num = num + 1
end 
```

### for 
```Lua
-- in general, range is begin, end [, step]

karlSum = 0
for i = 1, 100 do -- range includes start and stop 
	karlSum = karlSum + i
end 


-- one liner with step definition 
fredSum = 0
for j = 100, 1, -1 do fredSum = fredSum + j end 
```

### repeat...until
```Lua
num = 10

repeat 
	print('Hi')
	num = num - 1
until num == 0
```

# Functions 
functions may be normal, closures, and anonymous. Functions are
- first class 
- may be local/global

```Lua
function adder(x)
	-- the function thats returned is created when addr is called
	-- addr, remembers the value of x 
	return function (y) return x + y end 
end 
```

```Lua 
-- these functions are exactly the same 
local function g(x) return math.sin(x) end 
local g; g = function (x) return math.sin(x) end 
```

### Multiple Assignment 
returns, functions calls, and assignments all work with lists that may be mismatched in length. 

# Tables 
**muy importante**. Tables are Lua's only compound data structure - they are associative arrays. They are hash-lookup tables that can also be used as lists. 

### Using Tables as Dicts / maps: 
```Lua
t = {key1 = 'val1', key2 = false}
print(t.key1) -- value lookup 
t.newkey = {} -- adding k/v pair 
t.key2 = nil -- key removal 
```

### Assignments from keys 
```Lua 
u = {['1'] = 'qbert', [{}]= 1729}

a = u['1'] -- a = 'qbbert'
b = u[{}]  -- b = nill since the lookup fails. The lookup fails because the key used is not the same onject used to store the original value
```
*take-away: strings and numbers are the only portable keys*

### Single Table param function 
functions which take a single key as a function do not need parenthesis 
```Lua 
function h(x) print(x.key1) end 
h{key1 = 'test'} -- prints test
```

### Iterating over Tables
```Lua 
for key, val in pairs(u) do  -- Table iteration.
  print(key, val)
end
```

### _G (Global Tables)
`_G` is a special table of all global tables 
```Lua 
print(_G['_G'] == _G)  -- Prints 'true'.
```

### Implicit literals 
```Lua 
-- List literals implicitly set up int keys:
v = {'value1', 'value2', 1.21, 'gigawatts'}
for i = 1, #v do  -- #v is the size of v for lists.
  print(v[i])  -- Indices start at 1 !! SO CRAZY!
end
```
A 'list' is not a real type. v is just a table with consecutive integer keys, treated as a list.

### Metatables & Metamethods 
```Lua
f1 = {a = 1, b = 2}  -- Represents the fraction a/b.
f2 = {a = 2, b = 3

metafraction = {}
function metafraction.__add(f1, f2)
  sum = {}
  sum.b = f1.b * f2.b
  sum.a = f1.a * f2.b + f2.a * f1.b
  return sum
end

setmetatable(f1, metafraction)
setmetatable(f2, metafraction)

s = f1 + f2  -- call __add(f1, f2) on f1's metatable
```

# Class-like tables & Inheritance
classes are not a built in type. There are different ways to make them using tables and metatables 
```Lua 
-- Classes aren't built in; there are different ways
-- to make them using tables and metatables.

-- Explanation for this example is below it.

Dog = {}                                   -- 1.

function Dog:new()                         -- 2.
  newObj = {sound = 'woof'}                -- 3.
  self.__index = self                      -- 4.
  return setmetatable(newObj, self)        -- 5.
end

function Dog:makeSound()                   -- 6.
  print('I say ' .. self.sound)
end

mrDog = Dog:new()                          -- 7.
mrDog:makeSound()  -- 'I say woof'         -- 8.

-- 1. Dog acts like a class; it's really a table.
-- 2. function tablename:fn(...) is the same as
--    function tablename.fn(self, ...)
--    The : just adds a first arg called self.
--    Read 7 & 8 below for how self gets its value.
-- 3. newObj will be an instance of class Dog.
-- 4. self = the class being instantiated. Often
--    self = Dog, but inheritance can change it.
--    newObj gets self's functions when we set both
--    newObj's metatable and self's __index to self.
-- 5. Reminder: setmetatable returns its first arg.
-- 6. The : works as in 2, but this time we expect
--    self to be an instance instead of a class.
-- 7. Same as Dog.new(Dog), so self = Dog in new().
-- 8. Same as mrDog.makeSound(mrDog); self = mrDog.
```