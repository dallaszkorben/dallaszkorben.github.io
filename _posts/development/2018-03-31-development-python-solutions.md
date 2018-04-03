---
layout: post
published: true
mathjax: false
featured: false
comments: true

title: Python Solutions
modified: '2018-04-01'
description: Python solutions
blog: development
category: [Development, Python]
tags: [Development, Python]
---
# 1. Check if a string is multi-line

{% highlight bash linenos %}
my_string="""This string is
is multi-line
string
"""
if( "\n" in my_string):
    print("Multi-line")
else:
    print("Single-line")
{% endhighlight %}

<p class="console">Multi-line</p>


# 2. Form groups of list elements

{% highlight bash linenos %}
n=3                               #number of elements in a group
orig_list="abcdefghij" 
it=iter(orig_list) 
tuple_of_groups=zip(*[it] * n) 
for group in tuple_of_groups:
    print(group)
{% endhighlight %}
<p class="console">('a', 'b', 'c')
('d', 'e', 'f')
('g', 'h', 'i')
</p>


# 3. Filter out the duplicated elements (keep the order)

{% highlight bash linenos %}
orig_list="AABCAAADA" 
d=dict() 
new_list="".join([d.setdefault(c,c) for c in orig_list if c not in d]) 
print(new_list)
{% endhighlight %}
<p class="console">ABCD</p>


# 4. Convert all element in a list to integer

{% highlight bash linenos %}
a=["1”,  “2"]
l=list( map( int, a ) )    #list() is necessarry to got through the map
print(l)
{% endhighlight %}
<p class="console">[1, 2]</p>


# 5. Read not defined numbers of space separated values

{% highlight bash linenos %}
par1, *args=string.split()    # "par1" always have value but args list can be empty
print(args)
{% endhighlight %}
<p class="console">['par2', 'par3']</p>


# 6. Evaluate a string as Python expression - 1

{% highlight bash linenos %}
x="a;b;c"
method="split"                      # Python command
par=[';']                           # parameter of the command
print( getattr(x, method)(*par)  )
{% endhighlight %}
{% highlight terminal %}['a', 'b', 'c']{% endhighlight %}


# 7. Evaluate a string as Python expression - 2

{% highlight bash linenos %}
x="'a;b;c'"
method=".split(';')"
print(eval(x+method))
{% endhighlight %}
<p class="console">['a', 'b', 'c']</p>


# 8 Custom order of chars in a String

{% highlight bash linenos %}
S="Sorting1234"        # You need special order on this string:
                       # lowercase, uppercase, odd numbers, even numbers
s=sorted(S, key=lambda c: (-ord(c) >> 5, c in '02468', c))
print(*s, sep='')      # The order will be done by an Tuple with 3 elements
                       # 1st element: -4 => lowercase, -3 => uppercase, -2 numbers
                       # 2nd element: always False except in case of odd numbers
                       # 3rd element: the value
{% endhighlight %}
<p class="console">ginortS1324</p>

Alternative solution in the 3rd line:
<p class="console">s=sorted(S, key=lambda c: (1 if re.match("[a-z]", c) else 2 if re.match("[A-Z]", c) else 3, c in '02468', c))</p>


# 9. Transformation of a string

{% highlight bash linenos %}
import re
def square(match):
    number = int(match.group(0))
    return str(number**2)

print( re.sub(r"\d+", square, "1 2 3 4 5 6 7 8 9") )
{% endhighlight %}
<p class="console">1 4 9 16 25 36 49 64 81</p>


# 10. Checking valid roman numbers from 1-3999

{% highlight bash linenos %}
import re
regex_pattern = r"^M{0,3}(CM|CD|D?C{0,3})(XC|XL|L?X{0,3})(IX|IV|V?I{0,3})$"
print(str(bool(re.match(regex_pattern, input()))))
{% endhighlight %}


# 11. Print strings in a list in separate lines

{% highlight bash linenos %}
x=["a", "b", "c"]
print("\n".join(x))
{% endhighlight %}
<p class="console">a
b
c
</p>


# 12. Sort a list by specified column

{% highlight bash linenos %}
from operator import itemgetter
x = [
 ['4', '21', '1', '14', '2008-10-24 15:42:58'], 
 ['3', '22', '4', '2somename', '2008-10-24 15:22:03'], 
 ['5', '21', '3', '19', '2008-10-24 15:45:45'], 
 ['6', '21', '1', '1somename', '2008-10-24 15:45:49'], 
 ['7', '22', '3', '2somename', '2008-10-24 15:45:51']
]

x.sort(key=itemgetter(2))

for i in x:
    print(*i)

{% endhighlight %}
<p class="console">4 21 1 14 2008-10-24 15:42:58  
6 21 1 1somename 2008-10-24 15:45:49  
5 21 3 19 2008-10-24 15:45:45  
7 22 3 2somename 2008-10-24 15:45:51  
3 22 4 2somename 2008-10-24 15:22:03  
</p>
