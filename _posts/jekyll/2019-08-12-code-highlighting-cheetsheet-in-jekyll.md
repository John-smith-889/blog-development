---
layout: post
title: Code Highlighting and Formatting Cheetsheet in Jekyll
categories: [Jekyll]
tags: ["#html &nbsp; #markdown"]
comments: true
---
<p align="left"> <span style="color:darkblue; font-family:Calibri; font-size: 110%;"> <em> #html &nbsp;  #markdown </em></span> </p>

![background-picture]({{site.baseurl}}/assets/front-end.png)

Creating a blog demands using some amount of graphical motives. In this place formatting and graphical motives are aggregated, useful in creating visual aspect of a Jekyll website. To explore motives presented below go to [github repository](https://github.com/John-smith-889/blog) to "_posts" catalog, and open this post to look at code behind that.


<div style="line-height:60%;"> <br> </div>
<p style="
border:3px; 
border-style:solid; 
border-color:#42649c; 
padding: 1em;
width: 60%;
"
> <strong>Contents:</strong> 
<br>
<strong>1.</strong> Code highlighting, 
<br> 
<strong>2. </strong> Text formatting.
</p>


<div style="line-height:20%;"> <br> </div>
## 1. Code highlighting

### Code highlighting in markdown

``` html
<a class="sidebar-nav-item{% if page.url == node.url %} 
active{% endif %}" href="{{site.baseurl}}{{ node.url }}">{{ node.title }}</a>
```


<br>
### Code highlighting in markdown - python code snippet

``` python

class Singleton:
    def __new__(self):
        print("la")
        # check whether obcject (self) has attribute "instance"
        
        # if hasattr function is evaluated as FALSE (object self not have instance)
        if not hasattr(self, 'instance'):
            
            # new instance is created
            self.instance = super().__new__(self)
            # __new__ is a method which create new instance of class
            # super is a reference to parent class
            
        # if hasattr function is evaluated as TRUE, just return existing instance
        # (so no new instance will be created )
        return self.instance
        # so this line making that we will get the same object even if we want
        # to create next object
    
    def method_01(self):
        print("lala")
```






<br>
### Code highlighting in markdown with raw clause
``` html
{% raw %}
<a class="sidebar-nav-item{% if page.url == node.url %} 
active{% endif %}" href="{{site.baseurl}}{{ node.url }}">{{ node.title }}</a>
{% endraw %}
```


<br>
### Code highlighting in markdown showing markdown code
````md
{% raw %}
``` html
<a class="sidebar-nav-item{% if page.url == node.url %} 
active{% endif %}" href="{{site.baseurl}}{{ node.url }}">{{ node.title }}</a>
```
{% endraw %}
````



<br>
### Code highlighting in markdown - when language not recognized
``` make-background-white
print("Something")
```

``` make-background-white
Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gem. Ensure you have `plugins: [jekyll-paginate]` in your configuration file.  
```



<br>
### Rogue code highlighting in rectangle sharp frame

{% highlight python %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}




<br>
### Rogue code highlighting with code numeration

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}



<br>
### Some command line or small code snippets

`Code`

or

<code>
More code
</code>



<br>
### Html code block

<pre>
  <code class="html">
    puts "hello"
  </code>
</pre>




<br>
## 2. Text formatting


### Div container - annotations

<div class="message">
Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. 
</div>



<br>
### Border around text

<p style="
border:3px; 
border-style:solid; 
border-color:#bd4593; 
padding: 1em;"
>First example with text surrounded by a colored border.
<br>
This example also has multiple lines.
</p>


<br>
### Border around text with regulated width

<p style="
border:3px; 
border-style:solid; 
border-color:#bd4593; 
padding: 1em;
margin: 22px;
width: 50%;"  
>First example with text surrounded by a colored border.
<br>
This example also has multiple lines.
</p>



<br>
### Border around text with regulated width 2

<p style="
border:3px; 
border-style:solid; 
border-color:#42649c; 
padding: 1em;
margin: 22px;
width: 50%;"  
>First example with text surrounded by a colored border.
<br>
This example also has multiple lines.
</p>




<br>
### Border around text with regulated width and text wrapped

<p style="
border:3px; 
border-style:solid; 
border-color:#bd4593; 
padding: 1em;
margin: 22px;
width: 50%;
float: left;"  
>First example with text surrounded by a colored border.
<br>
This example also has multiple lines.
</p>

<!-- border - is the width of line -->
<!-- width - is the width of whole text box -->
<!-- float: left; - enable to set whole box to the side and text wrapping -->
<!-- margin - is the margin around text box -->



<!-- fancy line break with specified size -->
<div style="line-height:100%;"><br>
</div>
Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. Wrapped text. 






<br>
### Text area
<textarea>
This is where the user can enter text...
</textarea>



<br>
### Text area 2
<form action="//www.html.am/html-codes/textboxes/submitted.cfm">
<textarea name="myTextBox" cols="50" rows="5" style="border:3px double #bd4593">
Enter some text...
</textarea>
<br />
</form>


<br>
### Inline font change
<span style="color:black; font-family:Consolas; font-size: 80%;">
Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. 
</span>



<br>
### Inline font change 2
Roses are <span style="color:red; font-family:Georgia; font-size:2em;">red.</span>



<br>
### Markdown colored text

Some Markdown text with <span style="color:blue">some *blue* text</span>.



<br>
### Markdown colored text in div container

<div class="message">
Some Markdown text with <span style="color:blue">some blue text</span>. <br>
Some Markdown text with <span style="color:red">some red text</span>.
</div>



<br>
### Tekst with line on the left

  > Tekst with line <br> on the left

<br>
### Bullet points
* One point
* second point


<br>
### Special characters writing in html
&#123; <br>
&#37;  <br>
&#125; <br>
&nbsp; <br>
&#96;  <br>


<br>
### Text bolding
**bolded text**

or 

<strong>bolded text also</strong>


<br>
### Italicization
*italicized text*


<br>
### Abbreviations
<abbr title="HyperText Markup Langage">HTML</abbr>



<br>
### Citation
<cite>&mdash; Werner Heisenberg</cite>



<br>
### Deletion
<del>Deleted something</del>



<br>
### Insertion
<ins>inserted</ins>



<br>
### Superscription
Something<sup>text</sup>



<br>
### Subscription 
Something<sub>text</sub>


<br>
### Align attribute - text to left
<p align="left">This is some text in a paragraph.</p>


<br>
### Align attribute - text to center
<p align="center">This is some text in a paragraph.</p>



<br>
### Align attribute - text to right 
<p align="right">This is some text in a paragraph.</p>



<br>
### Linebreak with specified size
<div style="line-height:100%;">
    <br>
</div>
<!--  #space -->
<div style="line-height:20%;"> <br> </div>


<br>
### Bulletpoints 
* First bullet
* second
* third



<br>
### Numeration 
1. First number
2. second
3. third


<br>
### Table

<table>
  <thead>
    <tr>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>First</td>
    </tr>
    <tr>
      <td>Second</td>
    </tr>
    <tr>
      <td>Third</td>
    </tr>
  </tbody>
</table>




<br>
### Table 2

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Feature 1</th>
      <th>Feature 2</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>10</td>
      <td>14</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>First</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <td>Second</td>
      <td>4</td>
      <td>6</td>
    </tr>
    <tr>
      <td>Third</td>
      <td>4</td>
      <td>4</td>
    </tr>
  </tbody>
</table>


<br>
### Photo uploading

![background-picture]({{site.baseurl}}/assets/karina-vorozheeva-unsplash.png)

<br>
### Annotation
<div class="message">
Instructions are dedicated for Windows 10 <br>
Ruby version: 2.5.3 <br>
Jekyll version: 3.8.5 <br>
</div>


