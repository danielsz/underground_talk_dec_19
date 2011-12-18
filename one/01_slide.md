!SLIDE 
<link href='http://fonts.googleapis.com/css?family=Squada+One|Galdeano' rel='stylesheet' type='text/css'>
<link href='http://fonts.googleapis.com/css?family=Ubuntu+Mono|Droid+Sans+Mono' rel='stylesheet' type='text/css'>
# Metaprogramming from scratch #

!SLIDE 
Meta- (from Greek: μετά = "after", "beyond", "adjacent", "self"), is a prefix used in English (and other Greek-owing languages) to indicate a concept which is an abstraction from another concept, used to complete or add to the latter.

!SLIDE
<center><img src="aristotle_pic.jpg"></center>

!SLIDE 

* Programs that write programs
* Program that knows how to deal with its own languages constructs at runtime

!SLIDE bullets incremental

* Whatsinitforme?
* I code for a living. I have kids, you know.
* Do I really need to know these things?
* Frameworks, libraries, DSLs, etc.

!SLIDE

	@@@ ruby
	a.b

!SLIDE
Equivalent to:
	
	@@@ ruby
	a.b()

!SLIDE
Exercice 1: Make it compile
	 
	 @@@ruby
	  class Person  

 	    def name 
	    end

	    def name=()
 	    end
	  end

	  person = Person.new("Ronald")
	  p person.name
	  person.name = "Mike"
	  p person.name

!SLIDE execute

	@@@ ruby
	class Person
	   attr_accessor :name
	end
	person = Person.new
	person.name = "Mike"
	p person.name

!SLIDE execute

       @@@ ruby
       Class.method(:attr_accessor).owner

!SLIDE execute

       @@@ ruby
       Class.ancestors

!SLIDE execute
Classes are objects
	
	@@@ ruby
	a=Class.new	
	a.name

!SLIDE execute
	@@@ ruby
	a=Class.new
	Person=a
	a.name

The new class begins as an anonymous Class instance, but becomes a named class when it's assigned to a constant.	

!SLIDE execute

       @@@ ruby
       class Person
         p "hi"
       end

!SLIDE execute

       @@@ ruby
       class Person
       	 p self	     
       end 
       p self

!SLIDE 

       @@@ ruby
       class Person
       	 def self.speak
       	   #I'm a class method, or rather a singleton method on the Class instance that represents Person
         end   
         def speak
       	   #I'm an instance method
         end
       end

!SLIDE execute

	@@@ ruby
	module Features
	  def talk
	    "hi"
	  end  
	end
	class Person; end
	Person.extend Features
	Person.talk

!SLIDE

	@@@ ruby
	module Features
  	   def my_attr()
  	  end
	end

	class Person
  	   extend Features
  	   my_attr :name
	end

!SLIDE execute
       @@@ ruby
       class SomeClass
         define_method :some_method do Math::PI end
       end
       SomeClass.new.some_method


!SLIDE bullets incremental

* Query instance variables and methods of a particular class
* Define an instance variable or instance method. 

!SLIDE

Object model in ruby (copied from Smalltalk)
Dynamic dispatch, messages are sent to a receiver, resolution at runtime


!SLIDE execute
Object model

Everything is an object.

	@@@ ruby
	["hello", 3, Class, method(:p)].map {|x| x.class}


!SLIDE

State and behavior

An object has instance variables and an associated class
The class is a table of methods

Instance variables are private
Classes are open (live)

!SLIDE execute

       @@@ ruby
       class Person
       	     def say_something;  "hi";  end
       end

       person = Person.new       

       class Person
       	     def say_something;  "bye";  end
       end

       person.say_something

		
!SLIDE execute
Write a method that writes a method.

      	@@@ ruby
      	class Person
	      def one
	      	  def two
	    	  end
	      end	  
	    end	  
	
	person = Person.new
	person.two      

!SLIDE execute
define_method

	@@@ ruby
	class Person
	      def one
	      end
	      define_method :two do;end
	 end

	 person = Person.new
	 person.two

!SLIDE

The design of the Smalltalk object model is based on a set of simple rules that are applied uniformly.
The rules are the following ones:

 Rule 1. Everything is an object that has some private data.

 Rule 2. Every object is instance of a class.

 Rule 3. A class deﬁnes the behavior via public methods and the structure of its instances via instance variables which are private to the instances.

 Rule 4. Each class is inheriting its behavior and structure description from a single superclass.

 Rule 5. Objects only communicate via message passing (i.e., method invocation). When an object receives a message, the corresponding method is looked up in the class of the receiver, then if not found on this class continues in the class’s superclasses.

 Rule 6. The class Object is the root of the inheritance tree (in Squeak this is ProtoObject the class that represents objects understanding the smallest set of messages).

 Rule 7. Classes are instances too. They are instances of other classes called metaclasses.



