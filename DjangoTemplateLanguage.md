# Django Template Language

[Source](https://docs.djangoproject.com/en/2.0/ref/templates/language/)

## Variables look like this: {{ variable }}
When the template engine encounters a variable, it evaluates that variable and
replaces it with the result. Use a dot (.) to access attributes of a variable.
When the template system encounters a dot, it tries the following lookups, in
this order: Dictionary lookup, Attribute or method lookup, Numeric index lookup.
If the resulting value is callable, it is called with no arguments. The result
of the call becomes the template value.

example: {{ section.title }}, {{variable_name}} etc.

Note that “bar” in a template expression like {{ foo.bar }} will be interpreted
as a literal string and not using the value of the variable “bar”, if one
exists in the template context.

## Filters look like this: {{ name|lower }}
This displays the value of the {{ name }} variable after being filtered through
the lower filter, which converts text to lowercase. Use a pipe (|) to apply
a filter.

Filters can be “chained.” The output of one filter is applied to the next.
{{ text|escape|linebreaks }}

A filter argument looks like this: {{ bio|truncatewords:30 }} (display the first
30 words of the bio variable)

To join a list with commas and spaces you’d use {{ list|join:", " }}

check out escape filter it is a good deterrent against xss attacks!

[Built in filters](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/#ref-templates-builtins-filters)

You can also create your own custom template filters

## Tags look like this: {% tag %}
Some tags create text in the output, some control flow by performing loops or
logic, and some load external information into the template to be used by later
variables.

Some tags (like if and for) require beginning and ending tags
(i.e. {% tag %} ... tag contents ... {% endtag %})

[Built in tags](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/#ref-templates-builtins-tags)

example:
```
{% if athlete_list|length > 1 %}
   Team: {% for athlete in athlete_list %} ... {% endfor %}
{% else %}
   Athlete: {{ athlete_list.0.name }}
{% endif %}
```

Certain applications provide custom tag and filter libraries. To access them in
a template, ensure the application is in INSTALLED_APPS and then use the load
tag in a template, like:
```
{% load humanize %}

{{ 45000|intcomma }}
```

When you load a custom tag or filter library, the tags/filters are only made
available to the current template – not any parent or child templates along the
template-inheritance path.

## comment syntax: {# #}
This syntax can only be used for single-line comments (no newlines are
permitted between the {# and #} delimiters). If you need to comment out a
multiline portion of the template, see the comment tag.

## Template inheritance
Template inheritance allows you to build a base “skeleton” template that
contains all the common elements of your site and defines blocks that child
templates can override.

This template, which we’ll call base.html, defines a simple HTML skeleton
document that you might use for a simple two-column page. It’s the job of
“child” templates to fill the empty blocks with content.

{% block %} tag creates these blocks which can be filled in child templates.
All the block tag does is to tell the template engine that a child template may
override those portions of the template.

base.html
```
<html lang="en">
<head>
    <link rel="stylesheet" href="style.css" />
    <title>{% block title %}My amazing site{% endblock %}</title>
</head>

<body>
    <div id="sidebar">
        {% block sidebar %}
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/blog/">Blog</a></li>
        </ul>
        {% endblock %}
    </div>

    <div id="content">
        {% block content %}{% endblock %}
    </div>
</body>
</html>
```

A child template might look like this:
```
{% extends "base.html" %}

{% block title %}My amazing blog{% endblock %}

{% block content %}
{% for entry in blog_entries %}
    <h2>{{ entry.title }}</h2>
    <p>{{ entry.body }}</p>
{% endfor %}
{% endblock %}
```
The extends tag is the key here. It tells the template engine that this template
“extends” another template. When the template system evaluates this template,
first it locates the parent – in this case, “base.html”.

At that point, the template engine will notice the three block tags in base.html
and replace those blocks with the contents of the child template.

Note that since the child template didn’t define the sidebar block, the value
from the parent template is used instead. Content within a {% block %} tag in a
parent template is always used as a fallback.

One common way of using inheritance is the following three-level approach:

1) Create a base.html template that holds the main look-and-feel of your site.

2) Create a base_SECTIONNAME.html template for each “section” of your site.
For example, base_news.html, base_sports.html. These templates all extend
base.html and include section-specific styles/design.

3) Create individual templates for each type of page, such as a news article or
blog entry. These templates extend the appropriate section template.

Here are some tips for working with inheritance:

If you use {% extends %} in a template, it must be the first template tag in
that template. Template inheritance won’t work, otherwise.

More {% block %} tags in your base templates are better. Remember, child
templates don’t have to define all parent blocks, so you can fill in reasonable
defaults in a number of blocks, then only define the ones you need later.

If you need to get the content of the block from the parent template, the
{{ block.super }} variable will do the trick.

Variables created outside of a {% block %} using the template tag as syntax
can’t be used inside the block.

For extra readability, you can optionally give a name to your {% endblock %} tag.
For example:
```
{% block content %}
...
{% endblock content %}
```
