# Forms in Django

Django handles three distinct parts of the work involved in forms:
- creating HTML forms for the data
- receiving and processing submitted forms and data from the client
- preparing and restructuring data to make it ready for rendering

### Form
At the heart of this system of components is Django’s **Form** class (describes a form and determines how it works and appears). 

### Form field
Form class has fields, which map to html form elements. A form’s fields are themselves classes; they (field class) manage form data and perform validation when a form is submitted. A form field is represented to a user in the browser as an HTML “widget” - a piece of user interface machinery. Each field type has an appropriate default Widget class, but these can be overridden as required.

```
from django import forms

# Form class
class ContactForm(forms.Form): 
    # field,
    subject = forms.CharField(max_length=100)  
    
    # filed, changing the default widget associated with a field
    message = forms.CharField(widget=forms.Textarea) 
    
    # field,
    sender = forms.EmailField() 
    
    # field,
    cc_myself = forms.BooleanField(required=False) 
```
