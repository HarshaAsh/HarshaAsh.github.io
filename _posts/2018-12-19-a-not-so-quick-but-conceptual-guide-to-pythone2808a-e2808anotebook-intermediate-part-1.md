---
id: 593
title: A Not-so-Quick-but-Conceptual guide to Python — Notebook | Intermediate | Part 1
date: 2018-12-19T01:41:28+05:30
author: Tamoghna Saha
layout: post
guid: https://www.harshaash.com/?p=593
permalink: '/a-not-so-quick-but-conceptual-guide-to-python%e2%80%8a-%e2%80%8anotebook-intermediate-part-1/'
image: /wp-content/uploads/2018/12/python-intermediate.png
categories:
  - Python
tags:
  - data science
  - dictionary
  - else
  - exception
  - file
  - for
  - if
  - intermediate
  - jupyter
  - list
  - loops
  - python
  - set
  - tuple
  - while
---
<div class="wp-block-image">
  <figure class="aligncenter"><img loading="lazy" width="1024" height="261" src="https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-1024x261.png" alt="" class="wp-image-594" srcset="https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-1024x261.png 1024w, https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-300x76.png 300w, https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate-768x196.png 768w, https://www.harshaash.com/wp-content/uploads/2018/12/python-intermediate.png 1910w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>
</div>

Hi. As mentioned in my <a href="https://medium.com/@tamoghnasaha.22/a-quick-guide-to-python-notebook-beginners-6bbe3e2bb762" target="_blank" rel="noreferrer noopener">previous article</a>, I am now sharing the intermediate part of the Python Tutorial series. I decided to split this part up into 2. Part 1 covers:  
1. Data Types [list, tuple, dictionary, set, frozenset]  
2. Conditional statements and loops [if-elif-else, for, while, break, continue]  
3. File IO [read, write, append, close]  
4. Exception Handling [try/except, finally, assertion]

### More Data&nbsp;Types {#7178}

**List of immutable objects:**

  * bool
  * int
  * float
  * str
  * tuple
  * frozenset

**List of mutable objects:**

  * list
  * set
  * dict

### List {#93b7}

List is a type of **mutable** object in Python used to store an **indexed** list of item. It is created using **square brackets** with commas separating the items. A certain item from the list can be accessed using it’s index number.

An empty list is created using an empty pair of square brackets.

A list can contain items of a **single item type or multiple item type**. A list within a list is also possible which is used to represent 2D grids as Python, by default, lacks multi-dimensional array feature. But this can be achieved using **numpy** which we will discuss in our Advanced Notebook.

**NOTE: Strings can be indexed like a list**.

<pre class="wp-block-preformatted">>>> empty_list = []<br />>>> words = ['Python',3.6,['Up Next','Tuple']]<br /><br />>>> print(words[0])<br />>>> print(words[2][1])<br /><br />>>> print(words[1])<br />>>> words[1]=2.7<br />>>> print(words)</pre>

<pre class="wp-block-preformatted">## accessing items of string by index<br />&gt;&gt;&gt; short_form = "User Defined Function"<br />&gt;&gt;&gt; print("In our last class, we went through {}{}{}".format(short_form[0], short_form[5], short_form[13]))</pre>

<pre class="wp-block-preformatted">Python<br />Tuple<br />3.6<br />['Python', 2.7, ['Up Next', 'Tuple']]<br />In our last class, we went through UDF</pre>

<pre class="wp-block-preformatted">## basic list operations<br />&gt;&gt;&gt; num_list = [1,2,3]<br />&gt;&gt;&gt; print(num_list + [4,5,6])<br />&gt;&gt;&gt; print(num_list * 2)<br />&gt;&gt;&gt; print(4 in num_list)<br />&gt;&gt;&gt; print(9 not in num_list)<br />&gt;&gt;&gt; print(not 1 in num_list)</pre>

<pre class="wp-block-preformatted">[1, 2, 3, 4, 5, 6]<br />[1, 2, 3, 1, 2, 3]<br />False<br />True<br />False</pre>

<pre class="wp-block-preformatted"># list functions and methods<br />>>> num = [1,2,3]<br />>>> num.append(4)<br />>>> num.append([5,6])<br />>>> print(num)<br />>>> print(len(num))<br /><br />>>> num.extend([7,8,9])<br />>>> print(num)<br />>>> print(len(num))<br /><br />>>> index = 2<br />>>> num.insert(index, 2.5)<br />>>> print(num)<br />>>> print("-----------------------------")<br />>>> print(num.index(3))<br />>>> print(num.index(2.0))<br /><br />>>> num.remove([5,6])<br />>>> num.pop()<br />>>> print(num)<br /><br />>>> print(max(num))<br />>>> print(num.count(5))<br /><br />>>> num.reverse()<br />>>> print(num)</pre>

<pre class="wp-block-preformatted">[1, 2, 3, 4, [5, 6]]<br />5<br />[1, 2, 3, 4, [5, 6], 7, 8, 9]<br />8<br />[1, 2, 2.5, 3, 4, [5, 6], 7, 8, 9]<br />-----------------------------<br />3<br />1<br />[1, 2, 2.5, 3, 4, 7, 8]<br />8<br /><br />[8, 7, 4, 3, 2.5, 2, 1]</pre>

### Tuple {#1040}

Tuple is a **immutable** Python object created using **Parentheses** with commas separating the items which can be accessed using it’s index number.

It is just like list, except **you cannot modify or re-assign a value in the tuple. It will throw TypeError**.

An empty tuple can also be created in the same way you create empty list.

**NOTE: Tuples can also be created without using Parentheses, simply separated by commas.**

#### But when should we put parenthesis on tuples, and when we shouldn’t? {#b39c}

**Answer**: We use parentheses for **nested tuple**.

<pre class="wp-block-preformatted">>>> empty_tuple = ()<br /><br />>>> my_tuple = ("is", "my", "tuple")<br />>>> print(my_tuple[2])<br /><br />>>> also_my_tuple = 'is', 'this', 'one'<br />>>> print(also_my_tuple[3])</pre>

<pre class="wp-block-preformatted">tuple<br /><br />---------------------------------------------------------------------------<br />IndexError                                Traceback (most recent call last)<br />&lt;ipython-input-5-7a7df2b84a95> in &lt;module><br /><strong>      5</strong> <br /><strong>      6</strong> also_my_tuple = 'is', 'this', 'one'<br />----> 7 print(also_my_tuple[3])<br /><br />IndexError: tuple index out of range</pre>

### Dictionaries {#d99e}

Dictionaries are data structures used **to map keys to values**. Just like list, they are **mutable** and made using **curly brackets**.

Dictionaries can be indexed in the same way as lists, **using square brackets containing keys**. Trying to index a key that isn’t a part of the dictionary returns a **KeyError**.

The useful dictionary method is **get**. It does same thing as indexing, but if the key is not found in the dictionary, it returns **None** instead of throwing any error.

**NOTE: Only immutable objects can be used as keys to dictionaries.**

<pre class="wp-block-preformatted">>>> empty_dict = {}<br /><br />>>> my_dict = {"Joker":'Why so serious?', "Bane": [1,2,3], "Scarecrow": 0.05}<br />>>> print(my_dict["Joker"])<br /><br />>>> my_dict_again = {(1,2,3):[1,2,3], ('a','b','c'):['a','b','c']}<br />>>> print(my_dict_again[(1,2,3)])<br /><br />>>> my_dict_again[4] = 'd'<br />>>> print(my_dict_again)</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; print(empty_dict[0])</pre>

<pre class="wp-block-preformatted">Why so serious?<br />[1, 2, 3]<br />{(1, 2, 3): [1, 2, 3], ('a', 'b', 'c'): ['a', 'b', 'c'], 4: 'd'}<br /><br />---------------------------------------------------------------------------<br />KeyError                                  Traceback (most recent call last)<br />&lt;ipython-input-6-75e3176fb6bc> in &lt;module><br /><strong>     10</strong> print(my_dict_again)<br /><strong>     11</strong> <br />---> 12 print(empty_dict[0])<br /><br />KeyError: 0</pre>

Now see this.

<pre class="wp-block-preformatted">&gt;&gt;&gt; my_dict_error = {[1,2,3]:'a',}</pre>

<pre class="wp-block-preformatted">---------------------------------------------------------------------------<br />TypeError                                 Traceback (most recent call last)<br />&lt;ipython-input-8-859c69ec502a&gt; in &lt;module&gt;<br />----&gt; 1 my_dict_error = {[1,2,3]:'a',}<br /><br />TypeError: unhashable type: 'list'</pre>

#### What does this error&nbsp;mean? {#bfe0}

An object is **hashable** if it has a hash value which never changes during its lifetime (it needs hash() method). List is unhashable because it’s content can change over its lifetime.

**NOTE**: Don’t know about Hash function? Think about it as the fingerprint of a file in an encrypted format. For details, search in Google.

<pre class="wp-block-preformatted"># How about a dictionary within a dictionary?<br />>>> my_dict_yet_again = {0:"infinity", 1:{'a':[1,2]}, 'b':{2: (3,4)}}<br />>>> print(my_dict_yet_again)<br />>>> print(my_dict_yet_again[1]['a'])<br /><br /># Some dictionary functions<br />>>> print(1 in my_dict_yet_again) # check if a key is available in the dictionary<br />>>> print({'a':[1,2]} in my_dict_yet_again.values()) #check if the value is available in the dictionary<br /><br />>>> my_dict_yet_again[True]=False<br />>>> print(my_dict_yet_again)<br /><br />>>> print(my_dict_yet_again.get(1)) # get method<br />>>> print(my_dict_yet_again.get(2))<br />>>> print(my_dict_yet_again.get("True","True string is not available as key"))</pre>

<pre class="wp-block-preformatted">{0: 'infinity', 1: {'a': [1, 2]}, 'b': {2: (3, 4)}}<br />[1, 2]<br />True<br />True<br />{0: 'infinity', 1: False, 'b': {2: (3, 4)}}<br />False<br />None<br />True string is not available as key</pre>

### Set and Frozenset {#fb4a}

Sets are Python object similar to lists or dictionaries. They are created using **curly braces** or the **set function**. They are unordered, which means that they **can’t be indexed**. They **cannot contain duplicate elements**. Due to the way they’re stored, it’s **faster to check whether an item is part of a set**, rather than part of a list.

Instead of using **append** to add an item to a set, we use **add**. The method **remove** removes a specific element from a set but **pop** removes an arbitrary element.

<pre class="wp-block-preformatted">>>> my_set = set((2.7,"3.6"))<br />>>> also_my_set = {2.7, 3.6}<br />>>> my_frozenset = frozenset(("Python","2.7"))<br /><br />>>> my_set.add(6)<br />>>> print(my_set)<br />>>> print(my_frozenset)<br /><br />>>> my_set.remove(2.7)<br />>>> my_set.pop()<br />>>> print(my_set)</pre>

<pre class="wp-block-preformatted"># some additional operations<br />&gt;&gt;&gt; first = {1, 2, 3, 4, 5, 6}<br />&gt;&gt;&gt; second = {4, 5, 6, 7, 8, 9}<br />&gt;&gt;&gt; print(first | second)<br />&gt;&gt;&gt; print(first & second)<br />&gt;&gt;&gt; print(first - second)<br />&gt;&gt;&gt; print(second - first)<br />&gt;&gt;&gt; print(first ^ second)</pre>

<pre class="wp-block-preformatted">{'3.6', 2.7, 6}<br />frozenset({'2.7', 'Python'})<br />{6}<br />{1, 2, 3, 4, 5, 6, 7, 8, 9}<br />{4, 5, 6}<br />{1, 2, 3}<br />{8, 9, 7}<br />{1, 2, 3, 7, 8, 9}</pre>

#### So, what are the operations that can be performed on mutable and immutable objects in&nbsp;Python? {#10df}

Please check the answer in the notebook attached below.

### Conditional statements, loops {#9217}

#### if, elif,&nbsp;else {#cbce}

Python uses **if** statements to run code if a certain condition holds _True_, otherwise they aren’t.

**NOTE**: Python uses **indentation** (white space at the beginning of a line) to delimit blocks of code. Other languages, such as C, use curly braces to accomplish this, but in Python, indentation is mandatory; programs won’t work without it.

**To perform more complex checks**, _if_ statements can be **nested**, one inside the other. This means that the inner _if_ statement is the statement part of the outer one.

An **else** statement follows an _if_ statement, and contains code that is called when the _if_ statement evaluates to _False_.

The **elif** (short for else if) statement is a shortcut to use when **chaining if and else statements**. A series of _if elif_ statements can have a final else block, which is called if none of the _if_ or _elif_ expressions is _True_.

<pre class="wp-block-preformatted">&gt;&gt;&gt; num = int(input("Enter a number from 0 to 9: "))<br />&gt;&gt;&gt; if num == 3:<br />        print("You got 3")<br />    elif num == 6:<br />        print("Number is 6")<br />    elif num == 9:<br />        print("Looks like 9")<br />    else:<br />        print("`If you knew the magnificence of the three, six and nine, you would have a key to the universe.` ~ Tesla")</pre>

<pre class="wp-block-preformatted">Enter a number from 0 to 9: 5<br />`If you knew the magnificence of the three, six and nine, you would have a key to the universe.` ~ Tesla</pre>

#### for {#f3b3}

The **for** loop is commonly used to repeat some code a certain number of times on an object known as **iterator**. This is done by combining for loops with **range** objects.

The function range by default starts counting from 0 and goes up to the n-th value i.e., till (n-1). Its first parameter is the starting point, second one is the ending point (n-th value), and the optional third is the step value.

<pre class="wp-block-preformatted">&gt;&gt;&gt; for i in range(5):<br />        if i &lt; 3:<br />            print("hello!")<br />        else:<br />            print("world")<br />        <br />&gt;&gt;&gt; print("-----------------")<br />        <br />&gt;&gt;&gt; for i in range(2,12,3):<br />        print(i)</pre>

<pre class="wp-block-preformatted">hello!<br />hello!<br />hello!<br />world<br />world<br />-----------------<br />2<br />5<br />8<br />11</pre>

#### Two questions for you&nbsp;guys {#62a9}

  1. Ever wondered why people use _i_ in for loop?
  2. What is the difference between **range(x)** and **list(range(x))**?

<pre class="wp-block-preformatted">&gt;&gt;&gt; print(list(range(5)))<br />&gt;&gt;&gt; print(range(5))</pre>

<pre class="wp-block-preformatted">[0, 1, 2, 3, 4]<br />range(0, 5)</pre>

#### Answer {#d1f6}

  1. The i stands for the item to be accessed from any iterable or range object.
  2. When you execute&nbsp;_?range_, it will say that range returns an object that produces a sequence of integers from start (inclusive) to stop (exclusive) by step **without assigning indexes to the values**. Rather, it generates only one number at a time, relying on a **for** loop to request for the next item in the range to be seen. However, **list(range()) does assign indices** and hence allows you to see the full sequence of the numbers immediately, without the assistance of a _for_ loop. **_By the way, this happens only in Python 3._**

#### while {#5b73}

An **if** statement is **run once** if its condition evaluates to _True_. A **while** statement is similar, except that it can be **run more than once**. The statements inside it are repeatedly executed, as long as the condition holds _True_. Once it evaluates to False, the next section of code is executed.

The **infinite loop** is a special kind of while loop where the condition is always True and never stops iterating.

To end a while loop prematurely, the **break** statement can be used inside the loop.

When a **continue** statement is encountered, the code flow jumps back to the top of the loop, rather than stopping it completely (which is the job of _break)_. Basically it **stops the current iteration** and continues with the next one.

<pre class="wp-block-preformatted">>>> import time<br />>>> mewtwo_cp = 30<br />>>> umbreon_dark_pulse = 3<br />>>> fight = True<br />>>> print("You attacked Mewtwo! CP left: {}".format(mewtwo_cp))<br /><br />>>> while fight:<br />        print("Umbreon used Dark Pulse!\n")<br />        mewtwo_cp = mewtwo_cp - umbreon_dark_pulse<br />        <br />        if mewtwo_cp == 15:<br />            print("He's halfway dead!") <br />            continue<br />        elif mewtwo_cp == 9: <br />            print("Take him down!")<br />            continue<br />        elif mewtwo_cp == 3:<br />            print("Now's your chance") <br />            continue<br />        <br />        if mewtwo_cp &lt;= 0:<br />            print("Dead!")<br />            break<br />        <br />        print("Mewtwo CP left: {}".format(mewtwo_cp))<br />        time.sleep(1)<br />    <br />>>> print("Congrats! Your Umbreon won.")</pre>

<pre class="wp-block-preformatted">You attacked Mewtwo! CP left: 30<br />Umbreon used Dark Pulse!<br /><br />Mewtwo CP left: 27<br />Umbreon used Dark Pulse!<br /><br />Mewtwo CP left: 24<br />Umbreon used Dark Pulse!<br /><br />Mewtwo CP left: 21<br />Umbreon used Dark Pulse!<br /><br />Mewtwo CP left: 18<br />Umbreon used Dark Pulse!<br /><br />He's halfway dead!<br />Umbreon used Dark Pulse!<br /><br />Mewtwo CP left: 12<br />Umbreon used Dark Pulse!<br /><br />Take him down!<br />Umbreon used Dark Pulse!<br /><br />Mewtwo CP left: 6<br />Umbreon used Dark Pulse!<br /><br />Now's your chance<br />Umbreon used Dark Pulse!<br /><br />Dead!<br />Congrats! Your Umbreon won.</pre>

### File I/O {#edf9}

Python can be used to **read** and **write** the contents of files. Text files are the easiest to manipulate.

#### open {#c99e}

Before a file can be edited, it must be _opened_, using the **open** function. The **argument** of the open function is the _path to the file_. If the file is in the current working directory of the program, you can specify only its name.

#### mode {#bf80}

There are **mode** used to open a file by applying a _second argument_ to the open function.

  * “r” means open in **read** mode, which is the default.
  * “w” means **write** mode, for rewriting the contents of a file.
  * “a” means **append** mode, for adding new content to the end of the file.
  * “b” means **binary** mode, which is used for non-text files (such as image and sound files).

#### read {#80d8}

The contents of a file that has been opened in text mode can be read using the **read** method. To **read only a certain amount of a file, you can provide a number as an argument** to the read function. This determines the **number of bytes** that should be read.

After all contents in a file have been read, any attempts to read further from that file will return an _empty string_, because you are trying to read **from the end of the file**.

To retrieve **each line** in a file, you can use the **readlines** method to _return a list in which each element is a line in the file_.

**NOTE**: There is a **readline** and a **readlines** method. _readline()_ reads one line character at a time, _readlines()_ reads in the whole file at once and splits it by line.

#### write {#84d9}

To write to files we use the **write** method, which writes a string to the file. The “w” mode will _create a file, if it does not already exist_. When a file is opened in write mode, the file’s **existing content is deleted**. The write method **returns the number of bytes** written to a file, if successful.

**NOTE**: If you need to write anything other than string on a file, it has to be converted to a string first.

#### close {#b312}

Once a file has been opened and used, it should be closed which is done with the **close** method of the file object.

#### Alternative approach of file&nbsp;access {#6fb3}

An alternative way of doing it is using **with** statements. This creates a temporary variable (often called **_f_**_), which is only accessible in the indented block of the with statement._ **The file is automatically closed** at the end of the with statement, even if exceptions occur within it.

<pre class="wp-block-preformatted">&gt;&gt;&gt; file_name = open("def_NN.txt", "r")<br />&gt;&gt;&gt; print("------- Reading the content -------\n")<br />&gt;&gt;&gt; file_content = file_name.read()<br />&gt;&gt;&gt; print(file_content)<br />&gt;&gt;&gt; print("------- Re-reading -------")<br />&gt;&gt;&gt; print(file_name.read())<br />&gt;&gt;&gt; print("------- Finished! --------\n")<br />&gt;&gt;&gt; print("------- Closing the file -------")<br />&gt;&gt;&gt; file_name.close()<br /># try readlines</pre>

<pre class="wp-block-preformatted">------- Reading the content -------<br /><br />What is Neural Network?<br />A neural network is a processing unit that is capable to store knowledge and apply it to make predictions. A neural network mimics the brain in a way where the network acquires knowledge from its environment through a learning process. Then, intervention connection strengths known as synaptic weights are used to store the acquired knowledge. In the learning process, the synaptic weights of the network are modified in such a way so as to attain the desired objective.<br /><br />A neural network architecture comprises of 3 types of layers:<br /><br />Input Layer: The first layer in the network which receives input (training observations) and passed to the next hidden layer(s)<br />Hidden Layer: The intermediate processing layer(s) which perform specific tasks on the incoming data and pass on the output generated by them to the next output layer<br />Output Layer: The final layer of the network which generates the desired output<br />Each of these layers are composed of Perceptrons which is analogous to the neuron of the our nervous system.<br /><br />------- Re-reading -------<br /><br />------- Finished! --------<br /><br />------- Closing the file -------<br /></pre>

<pre class="wp-block-code"><code>>>> file_name = open("joker.txt", "r")
>>> print("------- Reading initial contents ------- \n")
>>> print(file_name.read())
>>> print("------- Finished ------- \n")
>>> file_name.close()
>>> file_name = open("joker.txt", "w")
>>> amount_written = file_name.write("I believe whatever doesn't kill you simply makes you...stranger.")
>>> print("Amount of text written: {}\n".format(amount_written))
>>> file_name.close()
>>> file_name = open("joker.txt", "r")
>>> print("------- Reading new contents ------- \n")
>>> print(file_name.read())
>>> print("\n ------- Finished -------")
>>> file_name.close()</code></pre>

<pre class="wp-block-preformatted">------- Reading initial contents ------<br /><br />You see, in their last moment, people show you who they really are.<br /><br />------- Finished -------<br /><br />Amount of text written: 64<br /><br />------- Reading new contents -------<br /><br />I believe whatever doesn't kill you simply makes you...stranger.<br /><br />------- Finished -------<br /></pre>

<pre class="wp-block-code"><code># alternative approach
>>> with open("def_NN.txt") as f:
        print(f.read())</code></pre>

### Exception Handling {#ec9b}

#### Exception {#d712}

**Exception** occur when something goes wrong due to incorrect code syntax or logic or input. When an exception occurs, the program immediately stops and doesn’t executes any lines further.

_Different exceptions are raised for different reasons._ Some common exceptions are listed below:

  * **ImportError**: an import fails
  * **IndexError**: a list is indexed with an out-of-range number
  * **NameError**: an unknown variable is used
  * **SyntaxError**: the code can’t be parsed or processed properly
  * **TypeError**: a function is called on a value of an inappropriate type
  * **ValueError**: a function is called on a value of the correct type, but with an inappropriate value

Third-party libraries and modules define their own exceptions. Learn more about built-in exceptions <a href="https://docs.python.org/3.7/library/exceptions.html" rel="noreferrer noopener" target="_blank">here</a>

Here are some examples of different built-in exceptions.

<pre class="wp-block-code"><code>>>> list=[1,2,3] 
>>> print(list[3])
Traceback (most recent call last): File "&lt;stdin>", line 1, in &lt;module> 
IndexError: list index out of range 

>>> printf(a)
File "&lt;stdin>", line 1 printf a     
                             ^ 
SyntaxError: invalid syntax

>>> print(a)
Traceback (most recent call last): File "&lt;stdin>", line 1, in &lt;module> 
NameError: name 'a' is not defined 

>>> import tk Traceback 
(most recent call last): File "&lt;stdin>", line 1, in &lt;module>
ImportError: No module named tk 

>>> a=2+"hello"Traceback 
(most recent call last): File "&lt;stdin>", line 1, in &lt;module>
TypeError: unsupported operand type(s) for +: 'int' and 'str' 

>>> list.remove(0) 
Traceback (most recent call last): File "&lt;stdin>", line 1, in &lt;module> 
ValueError: list.remove(x): x not in list</code></pre>

#### Exception Handling {#364b}

To handle exceptions and call code when an exception occurs, we have to use a **try/except** statement.

#### try-except {#bb30}

The **try** block contains code that might throw an exception. If that exception occurs, the code in the try block stops executing, and the code in the **except** block is run. If no error occurs, the code in the except block doesn’t run.

A try statement can have multiple different except blocks to handle different exceptions. _Multiple exceptions can also be put into a single except block using_ **_parentheses_**_,_ to have the except block handle all of them.

An except statement without any exception specified will catch all errors. **However, this kind of coding should be avoided.** If you do this, you are going against the zen of Python.

Exception handling is particularly useful when

  * dealing with user input
  * sending stuff over network or saving large amounts of data, since issues happening with hardware like losing power or signal problems can happen

<pre class="wp-block-preformatted">&gt;&gt;&gt; try:<br />        variable = 10<br />        print(variable + "hello")<br />        num1 = 7<br />        num2 = 0<br />        print(num1 / num2)<br />        print("Done calculation")<br />    except ZeroDivisionError:<br />        print("An error occurred due to zero division")<br />    except (ValueError, TypeError):<br />        print("ERROR!")</pre>

<pre class="wp-block-preformatted">ERROR!</pre>

#### raise {#a267}

We can use **raise** to throw an exception **if a condition occurs**. The statement can be complemented with a custom exception.

<pre class="wp-block-preformatted">&gt;&gt;&gt; x = 12<br />&gt;&gt;&gt; if x &gt; 5:<br />        raise Exception('x should not exceed 5. The value of x was: {}'.format(x))</pre>

<pre class="wp-block-preformatted">---------------------------------------------------------------------------<br />Exception                                 Traceback (most recent call last)<br />&lt;ipython-input-5-b2de8492a496&gt; in &lt;module&gt;<br /><strong>      1</strong> x = 12<br /><strong>      2</strong> if x &gt; 5:<br />----&gt; 3     raise Exception('x should not exceed 5. The value of x was: {}'.format(x))<br /><br />Exception: x should not exceed 5. The value of x was: 12</pre>

#### else and&nbsp;finally {#9ab2}

Here using the else statement, you can instruct a program to execute a certain block of code **only in the absence of exceptions**.

To ensure some code runs no matter what errors occur, you can use a **finally** statement. The finally statement is placed at the bottom of a try/except statement and else statement, if any. This diagram explains the concept of try-except-else-finally.<figure class="wp-block-image">

![](https://cdn-images-1.medium.com/max/800/1*tEPpZX7606TlYlQ93t5Dug.png) </figure> 

<pre class="wp-block-preformatted">&gt;&gt;&gt; try:<br />        num_1 = 2<br />        num_2 = 5<br />        print(num_1/num_2)<br />    except ZeroDivisionError as error:<br />        print(error)<br />    else:<br />        try:<br />            with open('joker.txt') as file:<br />                read_data = file.readline()<br />                print(read_data)<br />        except FileNotFoundError as fnf_error:<br />            print(fnf_error)<br />    finally:<br />        print('Getting printed irrespective of any exceptions.')</pre>

<pre class="wp-block-preformatted">0.4<br />I believe whatever doesn't kill you simply makes you...stranger.<br />Getting printed irrespective of any exceptions.</pre>

<pre class="wp-block-preformatted">&gt;&gt;&gt; try:<br />        print(1)<br />        print(10 / 0)<br />    except ZeroDivisionError:<br />        print(error)<br />    finally:<br />        print("This is executed last!")</pre>

<pre class="wp-block-preformatted">1<br />This is executed last!<br /><br />---------------------------------------------------------------------------<br />ZeroDivisionError                         Traceback (most recent call last)<br />&lt;ipython-input-7-b26411555290> in &lt;module><br /><strong>      2</strong>     print(1)<br />----> 3     print(10 / 0)<br /><strong>      4</strong> except ZeroDivisionError:<br /><br />ZeroDivisionError: division by zero<br /><br />During handling of the above exception, another exception occurred:<br /><br />NameError                                 Traceback (most recent call last)<br />&lt;ipython-input-7-b26411555290> in &lt;module><br /><strong>      3</strong>     print(10 / 0)<br /><strong>      4</strong> except ZeroDivisionError:<br />----> 5     print(error)<br /><strong>      6</strong> finally:<br /><strong>      7</strong>     print("This is executed last!")<br /><br />NameError: name 'error' is not defined</pre>

#### **Why the exceptions messages are printed at the end of the output, not between “1” and “This is executed&nbsp;last”?** {#f249}

While catching the error for _print(10 / 0)_ the system found another exception in the **except** block, the undeclared variable _error_ raising **NameError** exception. So nothing was printed. This inner _NameError_ exception was uncaught by program and can only printed after finally block.

#### Assesrtion {#82c1}

An **assertion is a sanity-check** where an expression is tested, and if the result comes up false, an exception is raised. When it encounters an assert statement, Python evaluates the accompanying expression, which is expected to be true. If the expression is false, Python raises an **AssertionError** exception.

AssertionError exceptions can be caught and handled like any other exception using the try-except statement, but if not handled, this type of exception will terminate the program.

**But what makes assertion different from try/except?**

An assertion would stop the program from running (because you should fix that error or the program is useless), but an exception would let the program continue running (if you use else or finally). In other words, **exceptions address the robustness of your application** while **assertions address its correctness**.

Assertions should be used to check something that **should never happen** while an exception should be used to check something that **might happen**(something in which you don’t have control like user input).

**NOTE**: The rule is that use **assertions** when you are trying to **catch your own errors** (functions or data that are internal to your system), and **exceptions** when trying to **catch other people’s errors**.

<pre class="wp-block-preformatted">>>> def KelvinToFahrenheit(temp):<br />        assert (temp >= 0),"Colder than absolute zero? Go back to school. -_-"<br />        return ((temp - 273)*1.8) + 32<br /><br />>>> print(KelvinToFahrenheit(273))<br />>>> print(KelvinToFahrenheit(-5))<br />>>> print(KelvinToFahrenheit(373))</pre>

<pre class="wp-block-preformatted">32.0<br /><br />---------------------------------------------------------------------------<br />AssertionError                            Traceback (most recent call last)<br />&lt;ipython-input-8-832b1596a334> in &lt;module><br /><strong>      4</strong> <br /><strong>      5</strong> print(KelvinToFahrenheit(273))<br />----> 6 print(KelvinToFahrenheit(-5))<br /><strong>      7</strong> print(KelvinToFahrenheit(373))<br /><br />&lt;ipython-input-8-832b1596a334> in KelvinToFahrenheit(temp)<br /><strong>      1</strong> def KelvinToFahrenheit(temp):<br />----> 2     assert (temp >= 0),"Colder than absolute zero? Go back to school. -_-"<br /><strong>      3</strong>     return ((temp - 273)*1.8) + 32<br /><strong>      4</strong> <br /><strong>      5</strong> print(KelvinToFahrenheit(273))<br /><br />AssertionError: Colder than absolute zero? Go back to school. -_-</pre>

As mentioned in the previous article, I will be attaching the notebook at the end. So yeah, we have reached the end of this article.

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/Tamoghna-Saha/1a8e7ffde9e67359f58aa527fb45c91d">Gist</a>.
  </noscript>
</div>

I hope you guys have enjoyed this article. For any questions or doubts, please comment below and share your feedback on the notebook. Stay tuned for the part 2. Till then, keep coding!