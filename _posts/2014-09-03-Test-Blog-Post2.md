---
layout: post
title: One Line Post
category: Coding
tags: jekyll github rss
year: 2014
month: 9
day: 4
published: true
summary: A follow up post on how I built my blog
---
Tags: <i class="icon-tags"></i> {% for tag in page.tags %} <a href="/tags/{{ tag }}" title="View posts tagged with &quot;{{ tag }}&quot;"><u>{{ tag }}</u></a>  {% if forloop.last != true %} {% endif %} {% endfor %}
---

[This](http://contra.gr) is just a test blog post...

> I am trying out some stuff.

It's quite easy to learn how this works.

*This is **C#** Code Sample:*

```csharp
public class Contact
{
	public string FirstName {get;set;}
	//this is a comment
	public string LastName {get;set;}
}
```



```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```




