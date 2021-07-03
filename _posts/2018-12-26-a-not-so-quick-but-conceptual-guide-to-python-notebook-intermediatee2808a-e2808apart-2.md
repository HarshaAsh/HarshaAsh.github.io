---
id: 693
title: A Not-so-Quick-but-Conceptual guide to Python | Notebook | Intermediate — Part 2
date: 2018-12-26T12:15:36+05:30
author: Tamoghna Saha
layout: post
guid: https://www.harshaash.com/?p=693
permalink: '/a-not-so-quick-but-conceptual-guide-to-python-notebook-intermediate%e2%80%8a-%e2%80%8apart-2/'
image: /wp-content/uploads/2018/12/python-intermediate.png
categories:
  - Python
tags:
  - class
  - filter
  - generator
  - intermediate
  - iterator
  - lambda
  - list
  - list comprehension
  - map
  - object
  - oops
  - python
---
<figure class="wp-block-image"><img loading="lazy" width="1024" height="261" src="https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-1024x261.png" alt="" class="wp-image-594" srcset="https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-1024x261.png 1024w, https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-300x76.png 300w, https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-768x196.png 768w, https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate.png 1910w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure> 

Let me be honest. This notebook took me a lot more time than I excepted because I want my audience to understand the concepts of the some of the topics mentioned below in as granular level as possible, yet not making the notebook lengthy.

As promised, this is the part 2 of Python Intermediate of my Python Tutorial series. In this notebook, I have covered:  
1. List Slices and Comprehension  
2. Lambda  
3. Map, Filter & Reduce  
4. Decorator  
5. Class  
6. Iterable, Iterator and Generator

I have tried to explain the **<g class="gr_ gr\_23 gr-alert gr\_gramm gr\_inline\_cards gr\_run\_anim Punctuation only-del replaceWithoutSep" id="23" data-gr-id="23">Decorator</g>**<g class="gr_ gr\_23 gr-alert gr\_gramm gr\_inline\_cards gr\_disable\_anim_appear Punctuation only-del replaceWithoutSep" id="23" data-gr-id="23">,</g> **Iterator and Generator** in details. Before diving into this section, I highly recommend you guys to go through these articles if you haven’t.

[Python Notebook | Beginners](https://www.harshaash.com/python-tutorial-beginner/)  
[Python Notebook | Intermediate | Part 1](https://www.harshaash.com/a-not-so-quick-but-conceptual-guide-to-python%e2%80%8a-%e2%80%8anotebook-intermediate-part-1/)

### List Slices {#6f40}

**List slices**&nbsp;provides an advanced way of retrieving values from a list. Basic list slicing involves indexing a list with&nbsp;**two colon-separated integers**. These three arguments are&nbsp;_lower limit, upper limit and step_. This returns a new list containing all the values in the old list between the indices specified. By default, lower limit is at index 0, upper limit is at the last value and step is +1.

You can also take a step backwards. When&nbsp;**negative values**&nbsp;are used for the first and second values in a slice, they&nbsp;**count from the end of list**.

The indexing of the iterable item starts from 0 if we take it from left and -1 if we take it from the right.

**NOTE**: Slicing can also be done on&nbsp;**tuple**.

<pre class="wp-block-preformatted">>>> squares = [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]<br />>>> print(squares[:])<br />>>> print(squares[::2])<br />>>> print(squares[2:8:2])<br />>>> print(squares[6:])<br />>>> print(squares[4:14])<br />>>> print(squares[1:-2])<br />>>> print(squares[-5:-2])<br />>>> print(squares[7:1:-2])<br />>>> print(squares[::-1])</pre>

<pre class="wp-block-preformatted">[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]<br />[0, 4, 16, 36, 64]<br />[4, 16, 36]<br />[36, 49, 64, 81]<br />[16, 25, 36, 49, 64, 81]<br />[1, 4, 9, 16, 25, 36, 49]<br />[25, 36, 49]<br />[49, 25, 9]<br />[81, 64, 49, 36, 25, 16, 9, 4, 1, 0]</pre>

### List Comprehension {#ed82}

List comprehension is a useful way of quickly creating lists using simplified version of&nbsp;_for_&nbsp;loop statement. A list comprehension&nbsp;**can also contain an if statement**&nbsp;to enforce a condition on values in the list.

**NOTE**: Trying to create a list, by any means, in a very extensive range will result in a&nbsp;**MemoryError**.

<pre class="wp-block-code"><code>var = [2*i for i in range(10**100)]</code></pre>

#### DON’T EVEN TRY&nbsp;IT! {#4ffa}

<pre class="wp-block-preformatted">>>> evens=[i**2 for i in range(10) if i**2 % 2 == 0]<br />>>> print(evens)</pre>

<pre class="wp-block-preformatted">[0, 4, 16, 36, 64]</pre>

<pre class="wp-block-preformatted"># modify element of list by index value<br />>>> num = [1,2,3,4,5,6,7,8]<br />>>> list_of_index = [i for i in num if num.index(i)%2 == 0]<br />>>> print(list_of_index)<br />>>> even_num = [num[i] for i in list_of_index]<br />>>> print(even_num)</pre>

<pre class="wp-block-preformatted">[1, 3, 5, 7]<br />[2, 4, 6, 8]</pre>

### Lambda {#4353}

In Python,&nbsp;**anonymous function**&nbsp;means a function&nbsp;**without a name**, whereas we use&nbsp;_def_&nbsp;keyword to create normal functions. The&nbsp;**lambda**&nbsp;function is used for creating&nbsp;_small, one-time and anonymous_&nbsp;function objects in Python. The lambda operator can have&nbsp;**any number of arguments**, but it can have&nbsp;**only one expression**. The lambda functions can be assigned to variables, and used like normal functions.

Use lambda functions when an anonymous function is required for a short period of time.

<pre class="wp-block-preformatted">#named function<br />>>> def polynomial(x):<br />        '''<br />        Function to perform a polynomial calculation having a single    variable x<br />        '''<br />        return x**2 + 5*x + 4<br />>>> print("The result for named function: {}".format(polynomial(-4)))<br /></pre>

<pre class="wp-block-preformatted">#lambda<br />>>> poly = lambda x: x**2 + 5*x + 4<br />>>> print("The result for anonymous function: {}".format(poly(-4)))</pre>

<pre class="wp-block-preformatted">The result for named function: 0<br />The result for anonymous function: 0</pre>

### Map, Filter &&nbsp;Reduce {#a93b}

The built-in functions&nbsp;**map**,&nbsp;**filter**&nbsp;and&nbsp;**reduce**&nbsp;are very useful higher-order functions that operate on iterable.

The function&nbsp;**map**&nbsp;takes a function and an iterable as&nbsp;_arguments_, and returns a&nbsp;_new iterable_&nbsp;with the function applied to each argument.

The function&nbsp;**filter**&nbsp;filters an iterable by removing items that don’t match a&nbsp;**predicate (a function that returns ONLY Boolean True)**.

The function&nbsp;**reduce**&nbsp;applies a rolling computation to sequential pairs of values in a iterable i.e., wanted to compute the product of a list items, sum of tuple items.

**NOTE**: Both in map and filter, the result has to be explicitly converted to a list or tuple if you want to print it. Python 2 returns a list by default, but this was changed in Python 3 which returns map or filter object, hence the need for the list or tuple function.

<pre class="wp-block-preformatted">>>> def add_five(x):<br />        return x + 5<br /><br />>>> num_var = [11, 22, 33, 44, 55]<br />>>> map_result = list(map(add_five, num_var)) # map<br />>>> print(map_result)<br /><br />>>> filter_result = tuple(filter(lambda x: x%2==0, num_var)) # filter<br />>>> print(filter_result)<br /><br />>>> from functools import reduce<br />>>> reduce_result = reduce((lambda x, y: x*y), num_var) # reduce<br />>>> print(reduce_result)</pre>

<pre class="wp-block-preformatted">[16, 27, 38, 49, 60]<br />(22, 44)<br />19326120</pre>

<pre class="wp-block-preformatted"># check this out!<br />>>> mylist = [1,2,3,4,5]<br />>>> print(tuple(map(lambda x: x if x>2 else 0, mylist)))<br />>>> print(list(filter(lambda x: x if x>2 else 0, mylist)))</pre>

<pre class="wp-block-preformatted">(0, 0, 3, 4, 5)<br />[3, 4, 5]</pre>

### Decorator {#1230}

**Decorator**&nbsp;are functions which modify the functionality of another function. Let’s go one step at a time to understand decorator. In the beginner’s article, we have mentioned that Python’s function is a&nbsp;**first class object**&nbsp;which can be

  * dynamically created, destroyed
  * stored in a variable
  * passed to a function as a parameter
  * returned as a value from a function

We have already seen the first point to be valid in the beginner’s article. Let’s validate each of these remaining 3 point.

<pre class="wp-block-preformatted">## functions can be assigned to a variable<br />>>> def my_pymon(text): <br />        return "Let's go, {}".format(text.upper())<br />>>> i_choose_you = my_pymon<br />>>> print(i_choose_you('pykachu'))<br />>>> print("="*20)<br /><br />## functions can be passed as argument to another function<br />>>> def your_pymon(text):<br />        return f"{text}"<br />>>> def trainer_select(func):<br />        print(func("I choose you, 'char'mander")) <br />>>> trainer_select(your_pymon) <br />>>> print("="*20) <br /><br />## function returned as a value from another function <br />>>> def battle_began_with(mons):<br />        def who_won(someone):<br />            return f"In the battle, {someone} won against {mons}"<br />        return who_won<br />>>> battle = battle_began_with("'char'mander")("pykachu")<br />>>> print(battle)<br /></pre>

<pre class="wp-block-preformatted">Let's go, PYKACHU<br />====================<br />I choose you, 'char'mander<br />====================<br />In the battle, pykachu won against 'char'mander</pre>

**When you put the pair of parentheses after the function name in main of code, only then the function gets executed. If you don’t put parentheses after it, then it can be passed around and can be assigned to other variables without executing it.**

<pre class="wp-block-preformatted">>>> def my_decor(a_func):<br />        def wrapper_func():<br />            print("I am doing some boring work before executing a_func()")<br />            a_func()<br />            print("I am doing some boring work after executing a_func()")<br />        return wrapper_func<br /><br />>>> def a_function_requiring_decor():<br />        print("I am the function which needs some decoration!")<br /><br />>>> print(a_function_requiring_decor())<br /><br />>>> print("="*50)<br /><br />>>> a_function_requiring_decor = my_decor(a_function_requiring_decor) #the so-called decorator is happening here<br />>>> print(a_function_requiring_decor())</pre>

<pre class="wp-block-preformatted">I am the function which needs some decoration! <br />None <br />================================================== <br />I am doing some boring work before executing a_func() <br />I am the function which needs some decoration! <br />I am doing some boring work after executing a_func() <br />None</pre>

The variable&nbsp;**a\_function\_requiring_decor**&nbsp;is pointing to the&nbsp;**wrapper_func**inner function. We are&nbsp;**returning wrapper_func as a function**&nbsp;when we call&nbsp;**my\_decor(a\_function\_requiring\_decor)**. So,&nbsp;**decorator wraps a function, modifying its behavior**.

Another way to write these decorators is&nbsp;**using @ symbol**.

<pre class="wp-block-preformatted">>>> def my_decorator(func):<br />        def wrapper():<br />            print("Take the marker and write something on the board.")<br />            func()<br />            print("Well done!")<br />        return wrapper<br /><br />>>> <a rel="noreferrer noopener" href="http://twitter.com/my_decorator" target="_blank">@my_decorator</a><br />>>> def tricky():<br />        print("SOMETHING!")<br /><br />>>> tricky()</pre>

<pre class="wp-block-preformatted">Take the marker and write something on the board.<br />SOMETHING!<br />Well done!</pre>

### Class {#50b0}

Python is an&nbsp;_object-oriented programming_&nbsp;(OOP) language and objects are created using&nbsp;**class**&nbsp;which is actually the focal point of OOP. The class describes an object’s blueprint, description or metadata. Multiple object can be instantiated using the&nbsp;_same class_.

Classes are created using the keyword&nbsp;**class**&nbsp;and an indented block, which contains class&nbsp;_methods_.

Let’s take a look at an example.

<pre class="wp-block-preformatted">>>> class Pet:<br />        def __init__(self, genre, name, owner):<br />            self.genre = genre <br />            self.name = name<br />            self.owner = owner<br />        <br />        def voice(self): #another method added to the class Pet<br />            print("Growl!")<br />        <br />>>> pokemon = Pet("dog","Arcanine","Tim")<br />>>> print(pokemon.name)<br />>>> pokemon.voice()</pre>

<pre class="wp-block-preformatted">Arcanine<br />Growl!</pre>

The&nbsp;**__ init__**&nbsp;method is the most important method in a class which is called when an instance (object) of the class is created.&nbsp;**All methods must have self as their first parameter**, although you do not need to pass it explicitly when you call the method.

Within the method definition,&nbsp;**self**&nbsp;refers to the object itself calling the method. From the above example, we see that

<pre class="wp-block-code"><code>pokemon = Pet("dog","Arcanine","Tim")
print(pokemon.name)
>>> Arcanine</code></pre>

  * When we create the pokemon object from the class Pet, we are passing&nbsp;_genre, name and owner_&nbsp;as “dog”,”Arcanine”,”Tim” and the object (pokemon) will take the place of self.
  * The attributes are accessed using the&nbsp;**dot**&nbsp;operator.
  * So&nbsp;**pokemon is the object**, “_Arcanine_” is the value of the&nbsp;**name**&nbsp;attribute of this object.

Hence, we can access the attributes in a class using this way:&nbsp;**object.attributes**.

Classes can have other methods defined to add functionality to them. These methods are accessed using the same dot syntax as attributes.

**NOTE**: All methods&nbsp;**must have self**&nbsp;as their first parameter.

Trying to access an attribute of an instance that isn’t defined causes an&nbsp;**AttributeError**.

### Iterable, Iterator and Generator {#bb8a}

#### Iterable and&nbsp;Iterator {#f66c}

Iteration -> Repetition of a process.

**Iterable**&nbsp;is a type of object which would&nbsp;**generate an Iterator**&nbsp;when passed to in-built method&nbsp;**iter()**.

**Iterator**&nbsp;is an object which is used to iterate over an&nbsp;_iterable object_&nbsp;using&nbsp;**next**() method, which returns the next item of the&nbsp;_iterable object_. Any object that has a&nbsp;**next**() method is therefore an iterator.

**NOTE**: List, Tuple, Set, Frozenset, Dictionary are in-built&nbsp;**iterable objects**. They are&nbsp;**iterable containers**&nbsp;from which you can get an&nbsp;**iterator**.

This is what happens.<figure class="wp-block-image">

![](https://cdn-images-1.medium.com/max/800/1*9l5bpqRGEa4LNLg3WTISPg.png) </figure> 

<pre class="wp-block-preformatted">## Let's see an example<br />>>> my_tuple = ["apple", "banana", "cherry"]<br />>>> iterated_tuple = iter(my_tuple)<br /><br />>>> print(type(iterated_tuple))<br />>>> print(next(iterated_tuple))<br />>>> print(next(iterated_tuple))<br />>>> print(next(iterated_tuple)</pre>

<pre class="wp-block-preformatted">&lt;class 'list_iterator'&gt;<br />apple<br />banana<br />cherry</pre>

<pre class="wp-block-preformatted">## same thing can be written using for loop<br />>>> my_tuple = ("apple", "banana", "cherry")<br />>>> for i in my_tuple:<br />        print(i)</pre>

<pre class="wp-block-preformatted">apple<br />banana<br />cherry</pre>

**How for loop actually works?**

The for loop can iterate over any iterable.

<pre class="wp-block-code"><code>for element in iterable:    
    # do something with element</code></pre>

is actually implemented as

<pre class="wp-block-code"><code># create an iterator object from that iterable
iter_obj = iter(iterable)

# infinite loop
while True:    
    try:        
        # get the next item
        element = next(iter_obj)
        # do something with element    
    except StopIteration:        
         # if StopIteration is raised, break from loop        
         break</code></pre>

  * The for loop creates an iterator object internally,&nbsp;**iter_obj**&nbsp;by calling&nbsp;_iter()_on the iterable.
  * Inside the&nbsp;**while loop**, it calls&nbsp;_next()_&nbsp;to get the next element and executes further
  * After all the items exhaust,&nbsp;**StopIteration**&nbsp;exception is raised which is internally caught and the loop ends.

To get a better sense of the internals of an iterator, let’s build an iterator producing the&nbsp;**Fibonacci numbers**.

<pre class="wp-block-preformatted">>>> from itertools import islice<br />>>> class fib:<br />         def __init__(self):<br />             self.prev = 0<br />             self.curr = 1<br /> <br />         def __iter__(self):<br />             return self<br /> <br />         def __next__(self):<br />             value = self.curr<br />             self.curr += self.prev<br />             self.prev = value<br />             return value<br />>>> f = fib()<br />>>> print(list(islice(f, 0, 10)))</pre>

<pre class="wp-block-preformatted">[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]</pre>

### Generator {#fa45}

A lot of overhead in building an iterator:

  * implement a class with iter() and next() methods
  * raise StopIteration when there was no values to be returned
  * makes the code lengthy

Python Generators are a simple way of creating iterators. All the above mentioned overhead are automatically handled by generators in Python.

**Generator**&nbsp;is a block of code, same as defining a function, having a&nbsp;**yield**statement instead of a&nbsp;**return**&nbsp;statement. If a function contains&nbsp;**at least one yield&nbsp;**statement (it may contain other yield or return statements), it becomes a generator!

The yield statement suspends function’s execution and sends a value back to caller, but retains enough capability to enable function to resume where it is left off. When resumed, the function continues execution immediately after the last yield run. This allows its code to produce a series of values over time, rather than computing them at once and sending them back like a list.&nbsp;**We should use yield when we want to iterate over a sequence, but don’t want to store the entire sequence in memory**.

This is how the above Fibonacci number code looks like using generator.

<pre class="wp-block-preformatted">>>> def fib():<br />        prev, curr = 0, 1<br />        while True:<br />            yield curr<br />            prev, curr = curr, prev + curr<br />>>> f = fib()<br />>>> print(list(islice(f, 0, 10)))</pre>

#### Let’s see what happened. {#7123}

Take note that&nbsp;**fib**&nbsp;is defined as a normal Python function, not as class. However, there’s&nbsp;**no return keyword**&nbsp;inside the function body.&nbsp;**The return value of the function will be a generator**.

  1. Now when&nbsp;**f = fib()**&nbsp;is called, the generator is instantiated and returned.&nbsp;**No code will be executed**&nbsp;at this point.To be explicit: the line prev, curr = 0, 1 is not executed yet.
  2. Then, this generator instance is wrapped in an islice(). This is itself also an iterator. Again, no code executed.
  3. Now, this iterator is wrapped in a&nbsp;**list()**, which will take the argument and build a list from it. To do so, it will start calling next() on the islice() instance, which in turn will start calling next() on our f instance.
  4. On the first call, the code&nbsp;**prev, curr = 0, 1**&nbsp;gets executed, then the&nbsp;**while True**&nbsp;loop is entered, and then it encounters the&nbsp;**yield curr**&nbsp;statement. It will produce the value that’s currently in the&nbsp;_curr_&nbsp;variable and become idle again. This value is passed to the&nbsp;_islice()_&nbsp;wrapper, which will produce the value (1 in this case) and list can add the value to the list.
  5. Then, list asks islice() for the next value, which will ask f for the next value, which will&nbsp;_unpause_&nbsp;f from its previous state, resuming with the statement&nbsp;**prev, curr = curr, prev + curr**.
  6. Then it re-enters the next iteration of the&nbsp;**while True**&nbsp;loop, and hits the&nbsp;**yield curr**&nbsp;statement, returning the next value of curr.
  7. This happens until the output list is 10 elements long. When list() asks islice() for the 11th value, islice() will raise a&nbsp;**StopIteration**&nbsp;exception, indicating that the end has been reached, and list will return the result: a list of 10 items, containing the first 10 Fibonacci numbers.

There are two types of generators in Python:&nbsp;**generator functions**&nbsp;and&nbsp;**generator expressions**. A generator function is any function in which the keyword&nbsp;**yield**&nbsp;appears in its body. We just saw an example of that. Generator expression is equivalent to list comprehension.

#### To avoid any confusion between iterable, iterator, generator, generator expression, a {list, set, dict} comprehension, check out this&nbsp;diagram. {#8c32}<figure class="wp-block-image">

<img loading="lazy" width="1024" height="462" src="https://www.harshaash.com/wp-content/uploads/2018/12/relationships-1024x462.png" alt="" class="wp-image-694" srcset="https://www.harshaash.com/wp-content/uploads/2018/12/relationships-1024x462.png 1024w, https://www.harshaash.com/wp-content/uploads/2018/12/relationships-300x135.png 300w, https://www.harshaash.com/wp-content/uploads/2018/12/relationships-768x347.png 768w, https://www.harshaash.com/wp-content/uploads/2018/12/relationships.png 1272w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

As always, I am attaching the notebook below.

I hope you have enjoyed this article. Stay tuned for the Python advanced. Peace.&nbsp;😉