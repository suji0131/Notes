# Forms in Django (add rest of notes for form as list etc.)
[Source](https://docs.djangoproject.com/en/2.0/topics/forms/)

Django handles three distinct parts of the work involved in forms:
- creating HTML forms for the data
- receiving and processing submitted forms and data from the client
- preparing and restructuring data to make it ready for rendering

## Basic Concepts
### Form
At the heart of this system of components is Django’s **Form** class (describes a form and determines how it works and appears). 

### Form field
Form class has fields, which map to html form elements. A form’s fields are themselves classes; they (field class) manage form data and perform validation when a form is submitted. A form field is represented to a user in the browser as an HTML “widget” - a piece of user interface machinery. Each field type has an appropriate default Widget class, but these can be overridden as required.

list of Django [fields](https://docs.djangoproject.com/en/2.0/ref/forms/fields/) and [widgets](https://docs.djangoproject.com/en/2.0/ref/forms/widgets/)

```
from django import forms

# Form class
class ContactForm(forms.Form): 

    # field 1,
    subject = forms.CharField(max_length=100)  
    
    # field 2, changing the default widget associated with a field
    message = forms.CharField(widget=forms.Textarea) 
    
    # field 3,
    sender = forms.EmailField() 
    
    # field 4,
    cc_myself = forms.BooleanField(required=False) 
```

## Step by Step Guide to building a form in Django

### 1) Create forms.py in the app

### 2) Write a form class, something like below
```
from django import forms

class NameForm(forms.Form):

    # creates a field with your_name
    your_name = forms.CharField(label='Your name', max_length=100)
    
#whole form when rendered will look like this:
<label for="your_name">Your name: </label>
<input id="your_name" type="text" name="your_name" maxlength="100" required />
```

Note that it does not include the ```<form>``` tags, or a submit button. We’ll have to provide those ourselves in the template.
    
### 3) Writing the view accordingly
To handle the form we need to instantiate it in the view for the URL where we want it to be published. Form data sent back to a Django website is processed by a view, generally the same view which published the form. This allows us to reuse some of the same logic.

```
from django.shortcuts import render
from django.http import HttpResponseRedirect

from .forms import NameForm

def get_name(request):
    # if this is a POST request we need to process the form data
    if request.method == 'POST':
        # create a form instance and populate it with data from the request:
        form = NameForm(request.POST)
        # check whether it's valid:
        if form.is_valid():
            # process the data in form.cleaned_data as required
            # ...
            # redirect to a new URL:
            return HttpResponseRedirect('/thanks/')

    # if a GET (or any other method) we'll create a blank form
    else:
        form = NameForm()

    return render(request, 'name.html', {'form': form})
```

### 4) Writing a Template
We don’t need to do much in our name.html template. The simplest example is:
```
<form action="/your-name/" method="post">
    {% csrf_token %} <!-- include this for the security -->
    {{ form }}
    <input type="submit" value="Submit" />
</form>
```

## Accessing Field Data
Lets consider the below forms.py which has 4 fields:
```
from django import forms

class ContactForm(forms.Form):
    subject = forms.CharField(max_length=100)
    message = forms.CharField(widget=forms.Textarea)
    sender = forms.EmailField()
    cc_myself = forms.BooleanField(required=False)
```
Whatever the data submitted with a form, once it has been successfully validated by calling ```is_valid()``` (and it returned True), the validated form data will be in the form.cleaned_data dictionary. This data will have been nicely converted into Python types for you.

Data can now be accessed using ```form.cleaned_data['field_name'] ```. Here’s how the form data could be processed in the view that handles this form:
```
#email example
from django.core.mail import send_mail

if form.is_valid():
    subject = form.cleaned_data['subject']
    message = form.cleaned_data['message']
    sender = form.cleaned_data['sender']
    cc_myself = form.cleaned_data['cc_myself']

    recipients = ['info@example.com']
    if cc_myself:
        recipients.append(sender)

    send_mail(subject, message, sender, recipients)
    return HttpResponseRedirect('/thanks/')
```


## Examples















