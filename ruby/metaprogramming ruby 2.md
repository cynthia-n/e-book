##The M Word
### 1) instance_methods(false)
>The class answered with an array containing a single method name: welcome. (The false argument means, “List only instance methods you defined yourself, not those ones you inherited.”) ```The "false" argument here means: ignore inherited methods```
  
***
  
### 2) my_object.instance_variables
>its instance variables
  
*** 

### 3) super "movies", ident
>调用父类的同名函数
>super不带括号表示调用父类的同名函数，并将本函数的所有参数传入父类的同名函数；super()带括号则表示调用父类的同名函数，但是不传入任何参数；
  
***
  
##Monday: The Object Model
### 4) Spell: Open Class
>When the previous code mentions class 'xxx' for the first time, no class by that name exists yet. So, Ruby steps in and defines the class and some methods. At the second mention, class 'xxx' already exists, so Ruby doesn’t need to define it. Instead, it reopens the existing class and defines other methods there.
>>you can always reopen existing classes— even standard library classes such as String or Array—and modify them on the fly
  
***
  
### 5) Spell: Monkeypatch
>if you casually add bits and pieces of functionality to classes. Some people would frown upon this kind of reckless patching of classes.```open class很有用，但是要小心，不要覆盖已有的方法，不然会出现很多问题```
  
>但Monkeypatch也不总是贬义的。It's quite useful when you do it on purpose—especially when you want to bend an existing library to your needs.
  
***
  
### 6) [].methods.grep /^re/
>gets a list of all methods in Ruby’s standard Array that begin with re；
>  
>Most objects inherit a number of methods from Object, so this list of methods is usually quite long. You can use Array#grep to filter.
  
***
  
### 7) What’s in an Object  
* Instance Variables
	* 实例变量和对两的类之间没有联系
	* 实例变量在给它们赋值时才会存在
	* 同一个类的不同对象的实例变量的键和值都可以不同
* Methods
	* Object#methods－－ You can get a list of an object’s methods
	* Instance methods are stored in the class, not the object（实例对象结构里并不存储方法，只存储实例变量和与类的关系）```Instance variables live in objects; methods live in classes.```
	* 类方法和实例方法区别。类方法类可以调用，实例对象不可调用；同理，实例方法实例对象可以调用，类不可调用。

>wrap up：  
>an object’s instance variables live in the object itself, and an object’s methods live in the object’s class. That’s why objects of the same class share methods but don’t share instance variables.
  
***
  
### 8) The Truth About Classes   
* classes themselves are nothing but objects -- 类本身只不过是对象。类是一个对象，所有适用于对象的类也适用于类。类和任何对象一样都有它自己的类, 类的类就是Class!` 
* you can call Class.new to create new classes while your program is running
* the methods of a class are the instance methods of Class
	* new -- you use it all the time to create objects
	* allocate -- plays a supporting role to new method(Chances are, you’ll never need to care about it)
	* superclass -- ```inheritance``` A Ruby class inherits from its superclass
	* Array < Object < BasicObject < nil
  
***
  
### 9) Modules 
>the superclass of Class --- a class is a module with three additional instance methods (new, allocate, and superclass) that allow you to create objects or arrange classes into hierarchies  

* 通过仔细地选择类或模块，可以使代码更加清晰.(make your intentions clear by using them for different purposes)
	* module -- pick a module when you mean it to be included somewhere
	* class -- pick a class when you mean it to be instantiated or inherited
  
***
  
### 10) my_class = MyClass 
>MyClass and my_class are both references to the same instance of Class  
>the only difference being that my_class is a variable, while MyClass is a constant.   
>```class names are nothing but constants```
  
***
  
### 11) Constants
* Ruby constant is actually very similar to a variable —- to the extent that(在一定程度上) you can change the value of a constant 
* The one important difference has to do with their scope
  
***
  
### 12) The Paths of Constants
* C::X －－ C class 中的常量 X（好比linux路径 /c/x）
* C中调用 ::X  C外层的常量 X（好比linux路径 ../x）
  
***
  
### 13) constants methods
> The Module class also provides an instance method and a class method  

* (实例方法)Module#constants returns all constants in the current scope(实例方法，类名常量等都是常量)
* (类方法)Module.constants returns all the top-level constants in the current program

  
***
  
### 14) Module.nesting
>if you need the current path, check out Module.nesting

```ruby
module M
  class C    module M2
      Module.nesting # => [M::C::M2, M::C, M]	 end
  endend
```
  
***
  
### 15) Spell: Namespace
>A module which only exists to be a container of constants, is called a Namespace.

```ruby
module Rake
  class Task
  end
end
```
'Task' had a good chance of clashing with other class names from different libraries. To prevent clashes, Rake switched to defining those classes inside a Rake module.Now the full name of the Task class is Rake::Task, which is unlikely to clash with someone else’s name.
  
***

### 16) require and load
>different purpose 

* You use load to execute code
* you use require to import libraries
  
***
  
### 17) 补充：require、load、include、extend、require_relative、autoload的区别 
####1.include  
```ruby
module Log
    def class_type
        "This class is of type: #{self.class}"
    end
end
class TestClass
    include Log
    # ...
end
tc = TestClass.new.class_type
```
将一个模块 include 到一个类中，相当于把模块中定义的代码插入到这个类中。  
> 一般用于类混入(Mixin)。秉持 DRY(Don't repeat yourself,字面意思来看,不要重复自己)原则，当多个类共享相同代码时，可以使用```include```方法处理.  

####2.load 
load(filename, wrap=false) -> true or raise LoadError

* filename可以是绝对路径，也可以是相对路径。Ruby不会为filename添加扩展名,加载文件要求必须带上扩展名；
* load会加载文件并执行，成功会返回true，找不到文件会抛出LoadError。
* load lib 时，不会保留痕迹，也就是可以多次 load (文件只會在第一次的時候載入,若再次 require 会忽略,而load每次一定會重新載入)。

>大多时候你都会使用 require ，除非你希望每次加载时都调用一次，那就用 load 。比如说你的 module 状态变化频繁，那你会希望每次类加载时都能反映变化，那就使用 load

```
load('motd.rb', true)
```
>You can force motd.rb to keep its constants to itself by passing a second, optional argument to load.  

* load('motd.rb') 加载执行motd.rb，但由于命名问题，可能会污染现有程序
* load('motd.rb', true) 强制给常量等增加命名空间。Ruby creates an anonymous module, uses that module as a Namespace to contain all the constants from motd.rb, and then destroys the module  

####3.require
require(name) -> true or false or raise LoadError

* Ruby会自动为name补充扩展名(.rb, .so, .etc)
* 第一次加载返回true，已经加载返回false，找不到文件会抛出LoadError。
* 找到该文件后，会运行该文件，并把该文件的绝对路径加入全局变量$"中，以此保证不重复加载

>require 可以让你 load 一个 library ，同时保证只能载入一次。建议你将 require 部分放到你的 .rb 程序文件的最上面。

####4.extend
extend 用来在一个对象（object，或者说是instance）中引入一个模块，这个类从而也具备了这个模块的方法。
同 include 的区别，extend 直接在 instance 实例对象的单间类中运行，等效于：  

```ruby
class << instance
    extend ‘xxxx’
end
```

例子:  

```ruby
module Mod
    def hello2
        "Hello from Mod.n"
    end
end

class Klass
    def hello
        "Hello from Klass.n"
    end
end

k = Klass.new
k.hello #"Hello from Klass.n"
k.hello2 # NoMethodError: undefined method `hello2
k.extend(Mod) 
# k.extend 这一句也可以修改为
class << k 
    include Mod 
end
k.hello2 #"Hello from Mod.n"
```
####5.require_relative  

与require相似却不同，区别在于文件路径查询。  

requrie filename  
>1）如果filename是一个相对路径，则会在$LAOD_PATH($:)中去寻找  
> $LOAD_PATH.unshift(File.dirname(__FILE__)) unless $LOAD_PATH.include?(File.dirname(__FILE__))   
> 其中File.dirname(__FILE__)代表当前路径，而$LOAD_PATH.unshift方法的目的就是将当前目录作用ruby标准的加载路径。  
> 2）如果filename是一个绝对路径，则寻找绝对路径  

require_relative filename   
> 1）直接取相对路径。此时与$LOAD_PATH($:)无关，是文件本身路径的相对地址。


####6.autoload  

autoload本质是会调用Kernel.require,但是又和require有区别。可以说autoload是一个smart的require...比require更加智能灵活。  

1) require 时文件立即执行。  
2) autoload  
```
autoload :MyLibrary, 'mylibrary'
```
> 使用autoload，只有使用到需要的常量或类文件才被加载。我们真正需要用某个文件时才加载，而require是直接加载，不管你是否会用到。
  
*** 

### 18) how objects and classes are related

![relation image](https://github.com/cynthia-n/e-book/raw/master/images/ruby/metaprogramming_ruby2/relation.png "how objects and classes are related")

