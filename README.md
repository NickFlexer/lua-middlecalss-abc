# lua-middlecalss-abc
Lua abstract base class implementation for middleclass 

### Overview
lua-middlecalss-abc is just an middleclass class. 
To mark methods as abstract it must return ```self.abstractmethod```
method ```ABC:set_abstract_methods(cls)``` set all abstract methods in abstract base class. You must mark one or more methods like abstract
metod ```ABC:check_abstract_methods(cls)``` check all methods of subclass. If some abstract methods not implemented ABC raise "Can't instantiate abstract class" error

### Simple example 

```lua
local class = require "middleclass"
local ABC = require "abc"

-- Defines an abstract base class
local AbstractClass = class("AbstractClass", ABC)

function AbstractClass:initialize()
    ABC.initialize(self)
    self:set_abstract_methods(AbstractClass)
end

function AbstractClass:first_method()
    return self.abstractmethod
end

function AbstractClass:second_method()
    return self.abstractmethod
end

-- Define class inheriting from our abstract class
local CorrectConcreteClass = class("CorrectConcreteClass", AbstractClass)

function CorrectConcreteClass:initialize()
    AbstractClass.initialize(self)
    self:check_abstract_methods(CorrectConcreteClass)
end

function CorrectConcreteClass:first_method()
    print("I'm correct first method!")
end

function CorrectConcreteClass:second_method()
    print("I'm correct second method!")
end
```

### Tests
lua-middlecalss-abc uses [busted](http://olivinelabs.com/busted/) for testing 

