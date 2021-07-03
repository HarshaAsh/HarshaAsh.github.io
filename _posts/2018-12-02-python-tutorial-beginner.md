---
id: 480
title: 'Get started with Python | Notebook for Beginner&#8217;s level'
date: 2018-12-02T19:58:52+05:30
author: Tamoghna Saha
layout: post
guid: https://www.harshaash.com/?p=480
permalink: /python-tutorial-beginner/
image: /wp-content/uploads/2018/11/python_beginner.png
categories:
  - Data Sciences
  - Python
tags:
  - analytics
  - jupyter
  - python
  - tutorial
---
<div id="container" class="site-main surface-container">
  <div class="butterBar butterBar--error" data-action-scope="_actionscope_1">
    <div class="screenContent surface-content is-supplementalPostContentLoaded" data-used="true" data-action-scope="_actionscope_2">
      <div class="notesMarkers" data-action-scope="_actionscope_4">
        <div class="branch-journeys-top">
          <div class="metabar-block u-flex1 u-flexCenter">
            <div class="u-xs-hide js-metabarLogoLeft">
              <div class="u-xs-hide js-metabarLogoLeft">
                <header class="container u-maxWidth740"> 
                
                <div class="uiScale uiScale-ui--regular uiScale-caption--regular u-paddingBottom10 row">
                  <div class="col u-size12of12 js-postMetaLockup">
                    <section class="section section--body section--first"> 
                    
                    <div class="section-content">
                      <div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*6Qh90O8nmW-6RZ1aYVL_ZQ.png" data-width="1920" data-height="500" data-is-featured="true" data-scroll="native">
                        <img class="progressiveMedia-image js-progressiveMedia-image" src="https://cdn-images-1.medium.com/max/2000/1*6Qh90O8nmW-6RZ1aYVL_ZQ.png" data-src="https://cdn-images-1.medium.com/max/2000/1*6Qh90O8nmW-6RZ1aYVL_ZQ.png" />
                      </div>
                    </div></section>
                  </div>
                </div></header>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="section-inner sectionLayout--fullWidth">
</div>

<div class="section-inner sectionLayout--insetColumn">
  <p id="ca11" class="graf graf--p graf-after--figure">
    Hi there. My name is <em>Tamoghna Saha, Harsha&#8217;s roomie</em>. For my bio, you can take a look at my <a href="https://www.linkedin.com/in/tamoghna-saha-12603a92">LinkedIn profile</a> or my <a href="https://github.com/Tamoghna-Saha">GitHub account</a>. He told me to take up the initiative of writing articles on data science on his website. I am not a &#8216;writing&#8217; kind of a guy but decided to give it a try. 😀
  </p>
  
  <p class="graf graf--p graf-after--figure">
    I have been working with Python for the past 2 years. There are lots of tutorials available online that covers Python, but sometimes it doesn’t cover the most crucial part which needs an answer:
  </p>
  
  <p class="graf graf--p graf-after--figure">
    “<em class="markup--em markup--p-em">Why do we need to use Python?</em>”<br /> “<em class="markup--em markup--p-em">Is it worth learning it?</em>”
  </p>
  
  <p id="01fa" class="graf graf--p graf-after--p">
    Since you have clicked this article, and reading till this point, I can assume that you are interested in Python or maybe you do know something about it but you need a quick recap. I am here to guide you not only with the syntax but also to tell some concepts, tips, and tricks associated with it.
  </p>
  
  <h3 id="2700" class="graf graf--h3 graf-after--p">
    Table of Content:
  </h3>
  
  <ul>
    <li>
      Numerical and Boolean Operations
    </li>
    <li>
      Variable and Object
    </li>
    <li>
      Data Type and Type Conversion
    </li>
    <li>
      Importing Python Modules and standard libraries
    </li>
    <li>
      Python Built-in Functions and keywords
    </li>
    <li>
      String operations and formatting
    </li>
    <li>
      Useful Pythonic Functions
    </li>
    <li>
      User-Defined Function
    </li>
    <li>
      Scope of a Variable
    </li>
  </ul>
  
  <ul class="postList">
    <li id="941c" class="graf graf--li graf-after--li">
      Additional Read
    </li>
  </ul>
  
  <h3 id="4300" class="graf graf--h3 graf-after--li">
    What is Python?
  </h3>
</div><figure id="d72e" class="graf graf--figure graf-after--h3"> 

<div class="aspectRatioPlaceholder is-locked">
  <div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded is-imageLoaded" data-image-id="1*89O4Cr0w6vGn67z8myuzww.png" data-width="612" data-height="306" data-scroll="native">
    <img loading="lazy" class="progressiveMedia-image js-progressiveMedia-image aligncenter" src="https://cdn-images-1.medium.com/max/800/1*89O4Cr0w6vGn67z8myuzww.png" alt="" width="612" height="306" data-src="https://cdn-images-1.medium.com/max/800/1*89O4Cr0w6vGn67z8myuzww.png" />
  </div>
</div></figure> 

<p id="edea" class="graf graf--p graf-after--figure">
  It is a general-purpose, high-level, interpreted, dynamic scripting language.
</p>

  * <strong class="markup--strong markup--li-strong">General-Purpose</strong> -> designed to be used for writing software in the widest variety of application domains
  * <strong class="markup--strong markup--li-strong">High-level</strong> -> designed to be more or less independent of a particular type of computer, human-readable friendly
  * <strong class="markup--strong markup--li-strong">Interpreted</strong> -> designed to execute instructions of a program directly, without previously compiling a program into machine-language instructions
  * <strong class="markup--strong markup--li-strong">Scripting</strong> -> languages which are interpreted rather than compiled

### But, what is the difference between an interpreter and a compiler? {#4690.graf.graf--h3.graf-after--li}<figure id="e54e" class="graf graf--figure graf--iframe graf-after--h3"> 

<div class="aspectRatioPlaceholder is-locked">
  <div class="progressiveMedia js-progressiveMedia is-canvasLoaded" data-scroll="native">
    <div class="oembed-gist">
      <noscript>
        View the code on <a href="https://gist.github.com/Tamoghna-Saha/606f1c5dda9e3a2b48ea7a6c135901a1">Gist</a>.
      </noscript>
    </div>
  </div>
</div></figure> 

### Currently, there are two versions of Python {#9a14.graf.graf--h3.graf-after--figure}<figure id="fab9" class="graf graf--figure graf-after--h3"> 

<div class="aspectRatioPlaceholder is-locked">
  <div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded" data-image-id="1*aW0qsCL6OYTd66n1bkMeMw.png" data-width="1600" data-height="691" data-action="zoom" data-action-value="1*aW0qsCL6OYTd66n1bkMeMw.png" data-scroll="native">
    <img loading="lazy" class="aligncenter wp-image-509 size-large" src="https://www.harshaash.com/wp-content/uploads/2018/11/Python-logo-1024x442.png" alt="" width="640" height="276" srcset="https://www.harshaash.com/wp-content/uploads/2018/11/Python-logo-1024x442.png 1024w, https://www.harshaash.com/wp-content/uploads/2018/11/Python-logo-300x130.png 300w, https://www.harshaash.com/wp-content/uploads/2018/11/Python-logo-768x332.png 768w, https://www.harshaash.com/wp-content/uploads/2018/11/Python-logo.png 1600w" sizes="(max-width: 640px) 100vw, 640px" />
  </div>
</div></figure> 

### Why do we need Python? {#c01c.graf.graf--h3.graf-after--figure}<figure id="54d1" class="graf graf--figure graf-after--h3"> 

<div class="aspectRatioPlaceholder is-locked">
  <div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded" data-image-id="1*FVNc5sE8cWIP0uluDUDluQ.jpeg" data-width="917" data-height="597" data-action="zoom" data-action-value="1*FVNc5sE8cWIP0uluDUDluQ.jpeg" data-scroll="native">
    <img loading="lazy" class="size-full wp-image-510 aligncenter" src="https://www.harshaash.com/wp-content/uploads/2018/11/Why_Python.jpg" alt="" width="917" height="597" srcset="https://www.harshaash.com/wp-content/uploads/2018/11/Why_Python.jpg 917w, https://www.harshaash.com/wp-content/uploads/2018/11/Why_Python-300x195.jpg 300w, https://www.harshaash.com/wp-content/uploads/2018/11/Why_Python-768x500.jpg 768w" sizes="(max-width: 917px) 100vw, 917px" />
  </div>
</div></figure> 

<div class="section-inner sectionLayout--insetColumn">
  <ul>
    <li>
      <strong class="markup--strong markup--li-strong">Simple syntax, readable, reusable and maintainable code</strong>
    </li>
    <li>
      <strong class="markup--strong markup--li-strong">Multiple Programming Paradigms</strong> such as Object-oriented, structured, functional Paradigms and feature of automatic memory management
    </li>
    <li>
      <strong class="markup--strong markup--li-strong">Compatible</strong> with Major Platforms and Systems, many <strong class="markup--strong markup--li-strong">open-source frameworks available</strong> which boost the developer’s productivity
    </li>
    <li>
      <strong class="markup--strong markup--li-strong">Robust Standard Library</strong> and supporting a wide range of external libraries
    </li>
  </ul>
  
  <ul class="postList">
    <li id="ee79" class="graf graf--li graf-after--li">
      Easier to perform coding and testing simultaneously by adopting <strong class="markup--strong markup--li-strong">test-driven development (TDD)</strong> approach
    </li>
  </ul>
  
  <h3 id="605d" class="graf graf--h3 graf-after--li">
    That’s okay. But where do I use it?
  </h3>
</div>

<div class="section-inner sectionLayout--outsetColumn">
  <figure id="8c0a" class="graf graf--figure graf--layoutOutsetCenter graf-after--h3" data-scroll="native"> 
  
  <div class="aspectRatioPlaceholder is-locked">
    <div class="progressiveMedia js-progressiveMedia graf-image is-canvasLoaded" data-image-id="1*1QgdIskGE1uATZwHGN7-zQ.jpeg" data-width="1152" data-height="623" data-action="zoom" data-action-value="1*1QgdIskGE1uATZwHGN7-zQ.jpeg" data-scroll="native">
      <img loading="lazy" class="aligncenter size-full wp-image-511" src="https://www.harshaash.com/wp-content/uploads/2018/11/application.jpg" alt="" width="1152" height="623" srcset="https://www.harshaash.com/wp-content/uploads/2018/11/application.jpg 1152w, https://www.harshaash.com/wp-content/uploads/2018/11/application-300x162.jpg 300w, https://www.harshaash.com/wp-content/uploads/2018/11/application-768x415.jpg 768w, https://www.harshaash.com/wp-content/uploads/2018/11/application-1024x554.jpg 1024w" sizes="(max-width: 1152px) 100vw, 1152px" />
    </div>
  </div></figure>
</div>

<div class="section-inner sectionLayout--insetColumn">
  <h3 id="ba08" class="graf graf--h3 graf-after--figure">
    Who uses Python anyway?
  </h3>
  
  <p>
    <img loading="lazy" class="aligncenter size-full wp-image-512" src="https://www.harshaash.com/wp-content/uploads/2018/11/who_uses_python.png" alt="" width="602" height="226" srcset="https://www.harshaash.com/wp-content/uploads/2018/11/who_uses_python.png 602w, https://www.harshaash.com/wp-content/uploads/2018/11/who_uses_python-300x113.png 300w" sizes="(max-width: 602px) 100vw, 602px" />
  </p>
</div>

### Cool. I guess we are good to go! {#e976.graf.graf--h3.graf-after--figure}

<pre id="2016" class="graf graf--pre graf-after--h3"># This is how you comment a code in Python!</pre>

<pre id="b173" class="graf graf--pre graf-after--pre"># Let’s start with the famous code.
&gt;&gt;&gt; print(‘Hello World’)

Hello World</pre>

<pre id="800c" class="graf graf--pre graf-after--pre"># a collection of 20 software principles that influences the design of Python Programming Language, of which 19 were written down
&gt;&gt;&gt; import this</pre>

<pre id="9391" class="graf graf--pre graf-after--pre">The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!

<em>In order to get an understanding of these aphorisms, take a look at this <a href="https://artifex.org/~hblanks/talks/2011/pep20_by_example.html">link</a>.</em></pre>

### Numerical and Boolean Operations {#d8f0.graf.graf--h3.graf-after--pre}

<pre id="e541" class="graf graf--pre graf-after--h3"># some basic mathematical operations , I am not showing. You do it. But see this.
&gt;&gt;&gt; print(25/4)
&gt;&gt;&gt; print(25//4)
&gt;&gt;&gt; print(25%4)
6.25
6
1</pre>

<pre id="244b" class="graf graf--pre graf-after--pre">&gt;&gt;&gt; x = 3
&gt;&gt;&gt; x *= 3 # in-place operator
&gt;&gt;&gt; print(x)
9</pre>

<pre id="870f" class="graf graf--pre graf-after--pre">&gt;&gt;&gt; y = “python”
&gt;&gt;&gt; y += “3”
&gt;&gt;&gt; print(y)
python3</pre>

In Python 3, `/` is called **floating-point division** and `//` is **floor division**. **But In Python 2.7, it will return the base integer (6 in this case) in both the divisions**.

Let&#8217;s look at some **Boolean operations**.

<p id="8b49" class="graf graf--p graf-after--pre">
  We will look into it. But let&#8217;s cover <strong class="markup--strong markup--p-strong">Boolean operations</strong>.
</p>

<pre class="graf graf--pre graf-after--p">&gt;&gt;&gt; from __future__ import division
&gt;&gt;&gt; print(“Easy ones!\n — — — — -”)
&gt;&gt;&gt; print(2 == 3)
&gt;&gt;&gt; print(6 != 7)
<span class="nb">&gt;&gt;&gt; print</span><span class="p">(</span><span class="mi">1</span> <span class="o">==</span> <span class="kc">True</span><span class="p">)</span>
<span class="nb">&gt;&gt;&gt; print</span><span class="p">(</span><span class="mi">2</span> <span class="o">==</span> <span class="kc">True</span><span class="p">)</span>
<span class="nb">&gt;&gt;&gt; print</span><span class="p">(</span><span class="mi">3</span> <span class="o">==</span> <span class="kc">False</span><span class="p">)
</span>&gt;&gt;&gt; print(9 is not “nine”) 
&gt;&gt;&gt; print(5 &gt; 3) 

Easy ones!
---------
False
True
True
False
False
True
True

&gt;&gt;&gt; print(“ — — — — -”) 
&gt;&gt;&gt; print(“Tricky ones!\n — — — — -”) 
&gt;&gt;&gt; print(6 &lt; 6.0) 
&gt;&gt;&gt; print((3 * 0.1) == 0.3) 
&gt;&gt;&gt; print((3 * 0.1) == (3/10))
--------- 
Tricky ones! 
--------- 
False 
False 
False</pre>

But how can the last two happen to be False? It should be True. The reason is very simple.

Floating point numbers are represented in computer hardware in **base 2**. Floating-point numbers are usually represented in **base 10**. _But most decimal fractions cannot be represented exactly as binary fractions._ As a result, the decimal floating-point numbers you enter are only **approximated** to the binary floating-point numbers actually stored in the machine.

No matter how many base-2 digits you are willing to use, the decimal value 0.1 cannot be represented **exactly** as a base 2 fraction.

Many users are not aware of the approximation because of the way values are displayed. If Python were to print the true decimal value of the binary approximation stored for 0.1, it would have to display

    >>> 0.1
    0.1000000000000000055511151231257827021181583404541015625

But this is more digits than most people find useful, so Python keeps the number of digits manageable by displaying a rounded value instead

    >>> 0.1
    0.1

So, even though the printed result looks like the exact value of 1/10, the _actual stored value is the **nearest representable binary fraction**_.

Note that this is in the _very nature of binary floating-point_: this is **NOT a bug in Python**. You’ll see the same kind of thing in all languages that support your hardware’s floating-point arithmetic. **The errors in Python float operations are inherited from the floating-point hardware.**

### Variables and Objects {#935e.graf.graf--h3.graf-after--pre}

Few things about variables:

  * Variables do not have a defined type at compile time.
  * Variables can reference any type of object!
  * Variable type can change in run-time.

Type checking is performed at run-time, and hence **dynamic languages are slower than static languages**.

**Everything in Python is an Object!** `object` is the base type for every Python Object. Objects can be:

  * **Mutable**: value can be changed. [list, set, dictionaries]
  * **Immutable**: value is unchangeable. [number, string, frozenset, tuple]

Object mutability is defined by its **type**. **They Are Never Explicitly Destroyed!** Allocation and deletion are done by the interpreter.

The most commonly used methods of constructing a multi-word variable name are as follows:

  * **Camel Case**: Second and subsequent words are capitalized, to make word boundaries easier to see. 
      * Example: numberOfCollegeGraduates
  * **Pascal Case**: Identical to Camel Case, except the first word is also capitalized. 
      * Example: NumberOfCollegeGraduates
  * **Snake Case**: Words are separated by underscores. 
      * Example: number\_of\_college_graduates

<pre id="c8d9" class="graf graf--pre graf-after--li"># the correct ways to declare variables 
&gt;&gt;&gt; my_variable = “is my variable, None of your variable"</pre>

<pre id="bbcd" class="graf graf--pre graf-after--pre"># definitely the wrong way to declare variables
&gt;&gt;&gt; 1234_get_on_the_dance_floor = "really?" # this is wrong. see what error you will get</pre>

### Data Type and Type Conversion {#a3ee.graf.graf--h3.graf-after--pre}

<pre id="b203" class="graf graf--pre graf-after--h3"># data types
&gt;&gt;&gt; print(type(“hello”))
&gt;&gt;&gt; print(type(True))
&gt;&gt;&gt; print(type(999.666))
&gt;&gt;&gt; print(type((-1+0j)))</pre>

<pre id="44ee" class="graf graf--pre graf-after--pre">&lt;class 'str'&gt;
&lt;class 'bool'&gt;
&lt;class 'float'&gt;
&lt;class 'complex'&gt;</pre>

<pre id="cc7a" class="graf graf--pre graf-after--pre"># type conversion
&gt;&gt;&gt; print(float(6))
&gt;&gt;&gt; print(str(99) + “ “ + str(type(str(99))))
&gt;&gt;&gt; print(int(“3”) + int(“6”))</pre>

<pre id="b0ea" class="graf graf--pre graf-after--pre">6.0
99 &lt;class 'str'&gt;
9</pre>

### Importing Python Modules and standard libraries {#ae05.graf.graf--h3.graf-after--pre}

<p id="f847" class="graf graf--p graf-after--h3">
  There are several ways to import standard and open-source external libraries to your programming environment:
</p>

<pre># 1. By directly import
&gt;&gt;&gt; import math
&gt;&gt;&gt; print(math.sin(45))
&gt;&gt;&gt; print("="*50)

# 2. By importing everything
&gt;&gt;&gt; from math import *

# 3. Using alias
&gt;&gt;&gt; import math as m

# 4. By specifically importing its functions
&gt;&gt;&gt; from math import sin, log
&gt;&gt;&gt; print(sin(45))
&gt;&gt;&gt; print(log(5))

</pre>

<pre>0.8509035245341184
==================================================
0.8509035245341184
1.6094379124341003</pre>

### Some of the default modules in Python {#0dff.graf.graf--h3.graf-after--pre}

  * <strong class="markup--strong markup--li-strong">sys</strong> -> System-specific parameters and functions.
  * <strong class="markup--strong markup--li-strong">io</strong> -> Core tools for working with streams.
  * <strong class="markup--strong markup--li-strong">os</strong> -> Miscellaneous operating system interfaces.
  * <strong class="markup--strong markup--li-strong">threading</strong> -> Higher-level threading interface.
  * <strong class="markup--strong markup--li-strong">multiprocess</strong> -> Process-based “threading“ interface.
  * <strong class="markup--strong markup--li-strong">socket</strong> -> Low — level networking interface.
  * <strong class="markup--strong markup--li-strong">asyncio</strong> -> Asynchronous I/O, event loop, coroutines, and tasks.
  * <strong class="markup--strong markup--li-strong">cmd</strong> -> Support for line-oriented command interpreters.
  * <strong class="markup--strong markup--li-strong">datetime</strong> -> Basic date and time types.
  * <strong class="markup--strong markup--li-strong">time</strong> -> Time access and conversions.
  * <strong class="markup--strong markup--li-strong">heapq</strong> -> Heap queue algorithm.
  * <strong class="markup--strong markup--li-strong">queue</strong> -> A synchronized queue class.
  * <strong class="markup--strong markup--li-strong">pathlib</strong> -> Object-oriented filesystem paths
  * <strong class="markup--strong markup--li-strong">math</strong> -> Mathematical functions

<ul class="postList">
  <li id="631e" class="graf graf--li graf-after--li">
    <strong class="markup--strong markup--li-strong">sqlite3</strong> -> DB — API interface for SQLite3 Databases.
  </li>
</ul>

### Python Built-in Functions and keywords {#8b72.graf.graf--h3.graf-after--li}

**Built-in functions** are core functions, provided by the Python Interpreter. These functions are **implemented in C** and hence are capable of using and manipulating Python objects at memory level, with increased performance.

**Keywords** are basically reserved words. It can&#8217;t be used as variable&#8217;s names.

<pre id="54d8" class="graf graf--pre graf-after--p"># built-in functions
&gt;&gt;&gt; builtin_functions_list = dir(__builtins__)
&gt;&gt;&gt; builtin_functions_data = np.array(builtin_functions_list)
&gt;&gt;&gt; shape = ((len(builtin_functions_list)//4),4)
&gt;&gt;&gt; print(tabulate(builtin_functions_data.reshape(shape), tablefmt='orgtbl'))</pre>

<pre id="81d6" class="graf graf--pre graf-after--pre">| ArithmeticError      | AssertionError         | AttributeError     | BaseException        
| BlockingIOError      | BrokenPipeError        | BufferError        | BytesWarning
| ChildProcessError    | ConnectionAbortedError | ConnectionError    | ConnectionRefusedError
| ConnectionResetError | DeprecationWarning     | EOFError           | Ellipsis             
| EnvironmentError     | Exception              | False              | FileExistsError
| FileNotFoundError    | FloatingPointError     | FutureWarning      | GeneratorExit        
| IOError              | ImportError            | ImportWarning      | IndentationError       
| IndexError           | InterruptedError       | IsADirectoryError  | KeyError
| KeyboardInterrupt    | LookupError            | MemoryError        | ModuleNotFoundError  
| NameError            | None                   | NotADirectoryError | NotImplemented         
| NotImplementedError  | OSError                | OverflowError      | PendingDeprecationWarning
| PermissionError      | ProcessLookupError     | RecursionError     | ReferenceError       
| ResourceWarning      | RuntimeError           | RuntimeWarning     | StopAsyncIteration     
| StopIteration        | SyntaxError            | SyntaxWarning      | SystemError               
| SystemExit           | TabError               | TimeoutError       | True                 
| TypeError            | UnboundLocalError      | UnicodeDecodeError | UnicodeEncodeError     
| UnicodeError         | UnicodeTranslateError  | UnicodeWarning     | UserWarning               
| ValueError           | Warning                | ZeroDivisionError  | __IPYTHON__          
| __build_class__      | __debug__              | __doc__            | __import__             
| __loader__           | __name__               | __package__        | __spec__                  
| abs                  | all                    | any                | ascii                
| bin                  | bool                   | bytearray          | bytes                  
| callable             | chr                    | classmethod        | compile                   
| complex              | copyright              | credits            | delattr              
| dict                 | dir                    | display            | divmod                 
| enumerate            | eval                   | exec               | filter                    
| float                | format                 | frozenset          | get_ipython          
| getattr              | globals                | hasattr            | hash                   
| help                 | hex                    | id                 | input                     
| int                  | isinstance             | issubclass         | iter                 
| len                  | license                | list               | locals                 
| map                  | max                    | memoryview         | min                       
| next                 | object                 | oct                | open                 
| ord                  | pow                    | print              | property               
| range                | repr                   | reversed           | round                     
| set                  | setattr                | slice              | sorted               
| staticmethod         | str                    | sum                | super                  
| tuple                | type                   | vars               | zip</pre>

<pre id="6a55" class="graf graf--pre graf-after--pre">### keywords
&gt;&gt;&gt; keywords_list = keyword.kwlist
&gt;&gt;&gt; keywords_data = np.array(keywords_list)
&gt;&gt;&gt; shape = ((len(keywords_list)//3),3)
&gt;&gt;&gt; print(tabulate(keywords_data.reshape(shape), tablefmt='orgtbl'))</pre>

<pre id="aca9" class="graf graf--pre graf-after--pre">| False | None   | True     |
| and   | as     | assert   |
| break | class  | continue |
| def   | del    | elif     |
| else  | except | finally  |
| for   | from   | global   |
| if    | import | in       |
| is    | lambda | nonlocal |
| not   | or     | pass     |
| raise | return | try      |
| while | with   | yield    |</pre>

### String operations and formatting {#f3eb.graf.graf--h3.graf-after--pre}

<pre id="7041" class="graf graf--pre graf-after--h3">## Concatenation
&gt;&gt;&gt; str_var_1 = "concatenation"
&gt;&gt;&gt; print("This is " + str_var_1 + " of string")
&gt;&gt;&gt; print(3*"3")
&gt;&gt;&gt; print("python"*3.7)
&gt;&gt;&gt; print("This will not print")</pre>

<pre id="20b3" class="graf graf--pre graf-after--pre">This is concatenation of string
333
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
&lt;ipython-input-15-6eae2c361731&gt; in &lt;module&gt;()
<strong class="markup--strong markup--pre-strong">      6</strong> print(3*"3")
<strong class="markup--strong markup--pre-strong">      7</strong> 
----&gt; 8 print("python"*3.7)
<strong class="markup--strong markup--pre-strong">      9</strong> 
<strong class="markup--strong markup--pre-strong">     10</strong> print("This will not print")

TypeError: can't multiply sequence by non-int of type 'float'</pre>

<pre id="693a" class="graf graf--pre graf-after--pre">## string formatting
# It provides a powerful way of embedding non-strings with strings

&gt;&gt;&gt; py_ver = "We are using Python version {}.{}.x".format(3,6)
&gt;&gt;&gt; print(py_ver)
&gt;&gt;&gt; other_version = 2.7
&gt;&gt;&gt; print(f"We could have also used Python {other_version}") # another way of performing string formatting
&gt;&gt;&gt; print("{0}{1}{0}".format("abra ","cad"))</pre>

<pre id="bc0c" class="graf graf--pre graf-after--pre">We are using Python version 3.6.x
We could have also used Python 2.7
abra cadabra</pre>

### Useful Pythonic Functions {#f6c8.graf.graf--h3.graf-after--pre}

<pre id="b8d5" class="graf graf--pre graf-after--h3"># strings
&gt;&gt;&gt; print(",".join(["NASA","Google","Netflix","Yahoo"]))
&gt;&gt;&gt; print("NASA-Google-Netflix-Yahoo".split("-"))
&gt;&gt;&gt; print("Python 2.7".replace("2.7","3.6"))
&gt;&gt;&gt; print("There is more to it than meets the eye".startswith("There")) # also endswith is there
&gt;&gt;&gt; print("python".upper())</pre>

<pre id="4e19" class="graf graf--pre graf-after--pre">NASA,Google,Netflix,Yahoo
['NASA', 'Google', 'Netflix', 'Yahoo']
Python 3.6
True
PYTHON</pre>

<pre id="7dba" class="graf graf--pre graf-after--pre"># numeric
&gt;&gt;&gt; print(max(10,64,86,13,98))
&gt;&gt;&gt; print(abs(-9))
&gt;&gt;&gt; print(sum([2,4,6,8]))</pre>

<pre id="1c08" class="graf graf--pre graf-after--pre">98
9
20</pre>

### User Input Function

There is no `raw_input` function in Python 3 as is available in Python 2. **By default, it expects string input**.

<pre># user input
data_input = int(input("Enter your ID: "))
print(type(data_input))
print("Employee having ID No: {} is late for office today.".format(data_input))

</pre>

<pre>Enter your ID: 7547857824
&lt;class 'int'&gt;
Employee having ID No: 7547857824 is late for office today.

# taking multiple input
name_var = input("Enter your name: ").split(" ")
print(name_var[0])
print(name_var[-1])

</pre>

<pre>Enter your name: bruce martha wayne
bruce
wayne</pre>

### User-Defined Function {#bf43.graf.graf--h3.graf-after--pre}

<p id="10fc" class="graf graf--p graf-after--h3">
  Before going ahead, can you tell me the difference between a function and a method? Well, here is the answer.
</p>

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/Tamoghna-Saha/49a08b555b9b551feb7eed679b8c44d2">Gist</a>.
  </noscript>
</div><section class="section section--body section--first"> 

<div class="section-content">
  <div class="section-inner sectionLayout--insetColumn">
    <figure id="0732" class="graf graf--figure graf--iframe graf-after--p"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="progressiveMedia js-progressiveMedia is-canvasLoaded" data-scroll="native">
      </div>
    </div></figure> 
    
    <p id="746c" class="graf graf--p graf-after--p">
      Create your own functions using <strong class="markup--strong markup--p-strong">def</strong> keyword.
    </p>
    
    <p id="a1f6" class="graf graf--p graf-after--p">
      UDF can either take or don’t take arguments. Technically, <strong class="markup--strong markup--p-strong">parameters</strong> are the variables in a function definition, and <strong class="markup--strong markup--p-strong">arguments</strong> are the values placed to the parameters when the function is called.
    </p>
    
    <p id="78b4" class="graf graf--p graf-after--p">
      The name of the UDF should be <strong class="markup--strong markup--p-strong">lowercase</strong>.
    </p>
    
    <p id="3b1e" class="graf graf--p graf-after--p">
      <strong class="markup--strong markup--p-strong">NOTE: You must define functions before they are called, in the same way, you declare a variable before using them</strong>
    </p>
    
    <pre id="0238" class="graf graf--pre graf-after--p">&gt;&gt;&gt; def udf_1(rqrdArg):
        return(3*rqrdArg)

&gt;&gt;&gt; def udf_2(optnlArg = None):
        print("OptionalArg: ", optnlArg)
    
&gt;&gt;&gt; def udf_3(rqrdArg, optnlArg=None, *args, **kwargs): # *args = extra unnamed argument, **kwargs = extra named arguments
        print("RequiredArg: ", rqrdArg)
        print("OptionalArg: ", optnlArg)
        print("Remaining Non-keyworded args: ",args)
        print("Remaining keyworded args: ",kwargs)

&gt;&gt;&gt; print("Calling UDF 1!")
&gt;&gt;&gt; print("RequiredArg: ", udf_1(5.7))

&gt;&gt;&gt; print("\nCalling UDF 2!")
&gt;&gt;&gt; udf_2()
&gt;&gt;&gt; udf_2(9)

&gt;&gt;&gt; print("\nCalling UDF 3!")
&gt;&gt;&gt; udf_3("Python","3.6",2,7,MSU_Python_Session=1)</pre>
    
    <pre id="eb77" class="graf graf--pre graf-after--pre">Calling UDF 1!
RequiredArg:  17.1

Calling UDF 2!
OptionalArg:  None
OptionalArg:  9

Calling UDF 3!
RequiredArg:  Python
OptionalArg:  3.6
Remaining Non-keyworded args:  (2, 7)
Remaining keyworded args:  {'MSU_Python_Session': 1}</pre>
    
    <pre id="04f2" class="graf graf--pre graf-after--p">&gt;&gt;&gt; def UDF_factorial(x):
        """
        This is a recursive function performing factorial of a number
        x -&gt; the number whose factorial is calculated
        """
        if x == 1:
            return 1
        else:
            return x * UDF_factorial(x-1)
    
&gt;&gt;&gt; print(UDF_factorial(5))

120</pre>
    
    <pre id="b7eb" class="graf graf--pre graf-after--pre"># how to check the function's docstring in notebook
&gt;&gt;&gt; ?UDF_factorial # (and execute)</pre>
    
    <p>
      <strong>*args</strong> and <strong>**kwargs</strong> allow one to pass a <strong>variable-length argument list</strong> and <strong>keyworded, variable-length argument dictionary </strong>respectively to a function when one doesn&#8217;t know beforehand how many arguments can be passed to the function.
    </p>
    
    <pre>&gt;&gt;&gt; def multiply(x,y):
        print(x*y)

&gt;&gt;&gt; multiply(3,9)
&gt;&gt;&gt; multiply(3,6,9)
27
---------------------------------------------------------------------------
TypeError Traceback (most recent call last)
&lt;ipython-input-24-999cf6ad6adb&gt; in &lt;module&gt;
3 
4 multiply(3,9)
----&gt; 5 multiply(3,6,9)

TypeError: multiply() takes 2 positional arguments but 3 were given

</pre>
    
    <pre># resolving the above issue with *args
&gt;&gt;&gt; def multiply(*args):
        x = 1
        for num in args:
            x *= num
            print(x)

&gt;&gt;&gt; multiply(4, 5)
&gt;&gt;&gt; multiply(10, 9)
&gt;&gt;&gt; multiply(2, 3, 4)
&gt;&gt;&gt; multiply(3, 5, 10, 6)
20
90
24
900

</pre>
    
    <pre># likewise for **kwargs
&gt;&gt;&gt; def print_kwargs(**kwargs):
        print(kwargs)

&gt;&gt;&gt; print_kwargs(kwargs_1="good stuffs", kwargs_2=2.7, kwargs_3=True)
{'kwargs_1': 'good stuffs', 'kwargs_2': 2.7, 'kwargs_3': True}

</pre>
    
    <p>
      When ordering arguments within a function or function call, arguments need to occur in a particular order:
    </p>
    
    <ol>
      <li>
        Formal positional arguments
      </li>
      <li>
        *args
      </li>
      <li>
        Keyword arguments
      </li>
      <li>
        **kwargs
      </li>
    </ol>
    
    <h3 id="1917" class="graf graf--h3 graf-after--pre">
      Scope of a variable
    </h3>
    
    <p id="d299" class="graf graf--p graf-after--h3">
      Not all variables are accessible from all parts of our program, and not all variables exist for the same amount of time.
    </p>
    
    <p id="7475" class="graf graf--p graf-after--p">
      A scope is a textual region of a Python program where a <strong class="markup--strong markup--p-strong">namespace</strong> is directly accessible. A namespace is a mapping from names (variables) to objects.
    </p>
    
    <p id="3e09" class="graf graf--p graf-after--p">
      Basically, part of a program where a variable is accessible is its <strong class="markup--strong markup--p-strong">scope</strong> and the duration for which the variable exists its <strong class="markup--strong markup--p-strong">lifetime</strong>.
    </p>
    
    <p id="1e78" class="graf graf--p graf-after--p">
      There are two types of variable scope:
    </p>
    
    <ul>
      <li>
        <strong class="markup--strong markup--li-strong">Global</strong>: It is defined in the main body of a file, will be visible throughout the file, and also inside any file which imports that file.
      </li>
    </ul>
    
    <ul class="postList">
      <li id="3cbd" class="graf graf--li graf-after--li">
        <strong class="markup--strong markup--li-strong">Local</strong>: it is defined inside a function, limiting its availability inside that function. It is accessible from the point at which it is defined until the end of the function and exists for as long as the function is executing.
      </li>
    </ul>
    
    <p id="d5c1" class="graf graf--p graf-after--li">
      In Python 3, the third type of variable scope has been defined — <strong class="markup--strong markup--p-strong">nonlocal</strong>. It allows to assign variables in an <strong class="markup--strong markup--p-strong">outer, but non-global</strong>, scope.
    </p>
    
    <pre id="7b03" class="graf graf--pre graf-after--p"># example showing global, local and nonlocal scopes
# global and local
&gt;&gt;&gt; x = "global"
&gt;&gt;&gt; def foo():
        print("x inside :", x)
&gt;&gt;&gt; foo()
&gt;&gt;&gt; print("x outside:", x)</pre>
    
    <pre id="4352" class="graf graf--pre graf-after--pre">x inside : global
x outside: global</pre>
    
    <pre id="5daa" class="graf graf--pre graf-after--pre">&gt;&gt;&gt; def func1():
        msg = "A"
        def func2():
            msg = "B"
            print(msg)
        func2()
        print(msg)
    
&gt;&gt;&gt; func1()</pre>
    
    <pre id="1c7a" class="graf graf--pre graf-after--pre">B
A</pre>
    
    <p>
      The <em>msg</em> variable is declared in the <strong>func1()</strong> function and assigned the value <em>&#8220;A&#8221;</em>. Then, in the <strong>func2()</strong> function, the value <em>&#8220;B&#8221;</em> is assigned to a variable having the same name <em>msg</em>.
    </p>
    
    <p>
      When we call the function <strong>func1()</strong>, it is, in turn, calling function <strong>func2()</strong> and <em>msg</em> variable in it has the value <em>&#8220;B&#8221;, but Python retains the old value of  &#8220;A&#8221;</em> in the <strong>func1()</strong> function.
    </p>
    
    <p>
      We see this behaviour because Python hasn’t actually assigned new value <em>&#8220;B&#8221;</em> to the existing <em>msg</em> variable, but has created a new variable called <strong>msg in the local scope of the inside function, that shadows the name of the variable in the outer scope</strong>.
    </p>
    
    <p>
      Preventing that behavior is where the nonlocal keyword comes in.
    </p>
    
    <pre class=""><code class="lang-none" data-language="none">&lt;span class="token keyword">def&lt;/span> &lt;span class="token function">func1&lt;/span>&lt;span class="token punctuation">(&lt;/span>&lt;span class="token punctuation">)&lt;/span>&lt;span class="token punctuation">:&lt;/span>
    msg &lt;span class="token operator">=&lt;/span> &lt;span class="token string">"A"&lt;/span>
    
    &lt;span class="token keyword">def&lt;/span> &lt;span class="token function">func2&lt;/span>&lt;span class="token punctuation">(&lt;/span>&lt;span class="token punctuation">)&lt;/span>&lt;span class="token punctuation">:&lt;/span>
        msg &lt;span class="token operator">=&lt;/span> &lt;span class="token string">"B"&lt;/span>
        
        &lt;span class="token keyword">def&lt;/span> &lt;span class="token function">func3&lt;/span>&lt;span class="token punctuation">(&lt;/span>&lt;span class="token punctuation">)&lt;/span>&lt;span class="token punctuation">:&lt;/span>
            nonlocal msg
            msg &lt;span class="token operator">=&lt;/span> &lt;span class="token string">"C"&lt;/span>
            &lt;span class="token keyword">print&lt;/span>&lt;span class="token punctuation">(&lt;/span>msg&lt;span class="token punctuation">)&lt;/span>
        func3&lt;span class="token punctuation">(&lt;/span>&lt;span class="token punctuation">)&lt;/span>
        &lt;span class="token keyword">print&lt;/span>&lt;span class="token punctuation">(&lt;/span>msg&lt;span class="token punctuation">)&lt;/span>
    
    func2&lt;span class="token punctuation">(&lt;/span>&lt;span class="token punctuation">)&lt;/span>
    &lt;span class="token keyword">print&lt;/span>&lt;span class="token punctuation">(&lt;/span>msg&lt;span class="token punctuation">)&lt;/span>
    
func1&lt;span class="token punctuation">(&lt;/span>&lt;span class="token punctuation">)&lt;/span></code></pre>
    
    <pre id="937d" class="graf graf--pre graf-after--pre">C
C
A</pre>
    
    <p>
      Now, by declaring <strong>nonlocal</strong> <em>msg</em> in the <strong>func3()</strong> function, Python knows that when it sees an assignment to msg, it should assign that value to the variable from the <strong>immediate</strong> outer scope <strong>instead of declaring a new variable that shadows its name</strong>.
    </p>
    
    <p>
      The usage of nonlocal is very similar to that of global, except that the former is used for <strong>variables in immediate outer function scopes</strong>.
    </p>
    
    <h3 id="6014" class="graf graf--h3 graf-after--p">
      Additional Read
    </h3>
    
    <ul>
      <li>
        <a class="markup--anchor markup--li-anchor" href="https://docs.python.org/3/tutorial/floatingpoint.html" target="_blank" rel="nofollow noopener noreferrer" data-href="https://docs.python.org/3/tutorial/floatingpoint.html">Floating Point Issue</a>
      </li>
      <li>
        <a class="markup--anchor markup--li-anchor" href="https://www.python.org/dev/peps/pep-0008/" target="_blank" rel="nofollow noopener noreferrer" data-href="https://www.python.org/dev/peps/pep-0008/">PEP0008 — Style Guide of Python</a>
      </li>
    </ul>
    
    <ul class="postList">
      <li id="b036" class="graf graf--li graf-after--li">
        <a class="markup--anchor markup--li-anchor" href="https://docs.python-guide.org/writing/style/" target="_blank" rel="nofollow noopener noreferrer" data-href="https://docs.python-guide.org/writing/style/">The Hitchhker’s Guide to Python — Writing Style</a>
      </li>
    </ul>
    
    <p id="42dc" class="graf graf--p graf-after--li graf--trailing">
      This is enough for the first part!
    </p>
  </div>
</div></section> 

<div class="postArticle-content js-postField js-notesSource js-trackedPost" data-post-id="6bbe3e2bb762" data-source="post_page" data-tracking-context="postPage" data-scroll="native">
  <section class="section section--body section--last"> 
  
  <div class="section-content">
    <div class="section-inner sectionLayout--insetColumn">
    </div>
  </div></section>
</div>

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/Tamoghna-Saha/19ef50d76191242fe23ae9592ec74570">Gist</a>.
  </noscript>
</div>

<div class="postArticle-content js-postField js-notesSource js-trackedPost" data-post-id="6bbe3e2bb762" data-source="post_page" data-tracking-context="postPage" data-scroll="native">
  <section class="section section--body section--last"> 
  
  <div class="section-content">
    <div class="section-inner sectionLayout--insetColumn">
      <p id="d697" class="graf graf--p graf-after--figure graf--trailing">
        I hope you guys have liked this article. We will meet in the 2nd part of this series.
      </p>
    </div>
  </div></section>
</div>