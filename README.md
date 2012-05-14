jinja-form-helper
=================

Set of macros used to help you create &lt;input>, &lt;select>, radio and checkbox  

### Why should I use this?
- You're from Rails and always miss those form helpers
- You don't want to write these tag directly because you are typo
- You don't know what the hell is this and want to give it a try!
- Make your template more readable! (maybe)

## How can I use this?
What you have to do is just place this file in *templates* directory  
and insert this line to your template file:

    {% import "macro.html" as f %}
    
then you can use macro from *f*

## Macros
You can pass as many keyword arguments as you want and it'll make element attributes for you
### label
label(for_name[, title])

    {{ f.label('name', 'First name')  }}
    # <label for='name' >First name</label>
    
    {{ f.label('name') }}
    # <label for='name'>Name</label>
    
    {{ f.label('name', class='label', id='name-label') }}
    # <label for='name' class='label' id='name-label' >Name</label>
    
### input_tag
input_tag(name, type='text')

    {{ f.input_tag('name', value='John') }}
    # <input name='name' type='text' value='John' />
    
    {{ f.input_tag('fileSelect', type='file') }}
    # <input name='fileSelect type='file' />
    
### input
Wrapper macro make it even more lazier!  
All keyword arguments will add to *input* tag  
input(name, type='text')

    {{ f.input('firstname') }}
    # <div class='group' >
    #   <label for'firstname' >Firstname</label>
    #   <input name='firstname' />
    # </div>
    
    {{ f.input('firstname', title='Last name!' value='Irving') }}
    # <div class='group' >
    #   <label for'firstname' >Last name!</label>
    #   <input name='firstname' value='Irving' />
    # </div>
    
### textarea_tag
textarea_tag(name, value="")

    {{ f.textarea_tag('feedback', 'Irving', class='textarea') }}
    # <textarea name='firstname' class='textarea' >Irving</textarea>
    
### textarea
Wrapper macro for those who lazy!  
textarea(name)

    {{ f.textarea('feedback', title='Fedback', value='Irving', class='textarea') }}
    # <div class='group' >
    #   <label for'feedback' >Fedback</label>
    #   <textarea name='feedback' class='textarea' >Irving</textarea>
    # </div>
    
### select_tag
select_tag(name, options, default=None)  
*options*: 2D-Array eg. [['m', 'Male'], ['f', 'Female']]  
*default*: must be the same type as first value in each options  

    {{ f.select_tag('gender', [['m', 'Male'], ['f', 'Female']]) }}
    # <select name="gender">
    #   <option value="m">Male</option>
    #   <option value="f">Female</option>
    # </select>
    
    {{ f.select_tag('gender', [['m', 'Male'], ['f', 'Female']], 'f') }}
    # <select name="gender">
    #   <option value="m">Male</option>
    #   <option value="f" selected="selected">Female</option>
    # </select>
    
### select
select(name, options, default=None)
*options*: 2D-Array eg. [['m', 'Male'], ['f', 'Female']]  
*default*: must be the same type as first value in each options  

    {{ f.select('gender', [['m', 'Male'], ['f', 'Female']], 'f', title='Gender') }}
    # <div class="group">
    # <label for="gender">Gender</label>
    # <select name="gender">
    #   <option value="m">Male</option>
    #   <option value="f" selected="selected">Female</option>
    # </select>
    # </div>

### checkbox_tag
checkbox_tag(name, options, checked=None)  
*options*: 2D-Array each item consists of value and label  
*checked*: Array stored checked value

    {{ f.checkbox_tag('test', [[1,'Male'], [2,'Female']], [1]) }}
    # <div class='checkboxs'>
    # <div class='checkbox-group' >
    # <label for='1'  >Male</label>
    #   <input name='test[]' type='checkbox' value='1' checked='checked' />
    # </div>
    # <div class='checkbox-group' >
    # <label for='2'  >Female</label>
    #   <input name='test[]' type='checkbox' value='2'  />
    # </div>
    # </div>
    
    {{ f.checkbox_tag('test', [[1,'Male'], [2,'Female']], [1,2], class='test') }}
    # <div class='checkboxs'>
    # <div class='checkbox-group' >
    # <label for='1'  >Male</label>
    #   <input name='test[]' type='checkbox' value='1' checked='checked' class='test'/>
    # </div>
    # <div class='checkbox-group' >
    # <label for='2'  >Female</label>
    #   <input name='test[]' type='checkbox' value='2' checked='checked' class='test'/>
    # </div>
    # </div>

### radio_tag  
checkbox_tag(name, options, default=None)  
*options*: 2D-Array each item consists of value and label  
*default*: a value that will be selected

    {{ f.radio_tag('test', [[1,'Male'], [2,'Female']], 1, class='test') }}
    # <div class='radios' >
    # <div class='radio-group' >
    # <label for='1'  >Male</label>
    #   <input name='test[]' type='radio' value='1' checked='checked' class='test'/>
    # </div>
    # <div class='radio-group' >
    # <label for='2'  >Female</label>
    #   <input name='test[]' type='radio' value='2'  class='test'/>
    # </div>
    # </div>

### button_tag  
button_tag(name, text, type='submit')  
*text*: text which will appear on the button if you don't supply one it'll use capitalized *name*  

    {{ f.button_tag('submit', 'Save')}}
    # <button name="submit" type="submit">Save</button>
    
    {{ f.button_tag('submit')}}
    # <button name="submit" type="submit">Submit</button>
