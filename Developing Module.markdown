<h1>E. Developing Odoo Module</h1>

In this tutorial, we will be developing a module called "**To-Do Application**", and the module will follow the Odoo way of 
developing modules.

Let's run through the development:

Step 1: Create a Directory and name the Directory "todo_app"

Step 2: Create an ```__init__.py``` file

Step 3: Create a ```__manifest__.py``` file and add the following:

```
{
    'name': 'To-Do Application',
    'description': 'Manage your personal To-Do tasks.',
    'author': 'Daniel Reis',
    'depends': ['base'],
    'application': True,
    }
```

Step 4: Install the Module

<h1>F. Enhancing To-do App</h1>

<h4>F1. Creating Data Model</h4>

The Odoo development guidelines state that the Python files for models should be placed inside a
models subdirectory. So let's create a ```todo_model.py``` and  ```__init__.py```and file in the model directory of the todo_app module.

Add the following content to the ```todo_model.py``` file:

```
from odoo import models, fields

class TodoTask(models.Model):
    _name = 'todo.task'
    _description = 'To-do Task'
    name = fields.Char('Description', required=True)
    is_done = fields.Boolean('Done?')
    active = fields.Boolean('Active?', default=True)
```

The first line is a Python code import statement, making available the models and fields objects
from the Odoo core.

The second line declares our new model. It's a class derived from models.Model .

The next line sets the **_name** attribute defining the identifier that will be used throughout Odoo to refer
to this model. Note that the actual Python class name, TodoTask in this case, is meaningless to other
Odoo modules. The **_name** value is what will be used as an identifier.

Right now, this file is not yet used by the module. We must tell Python to load it with the module in the
```__init__.py``` file. Let's edit it to add the following line:

```from . import todo_model```

That's it! For our Python code changes to take effect, the server instance needs to be restarted

<h4>F2. Creating View Layer</h4>

The view layer describes the user interface. Views are defined using XML, which is used by the web
client framework to generate data-aware HTML views.

The Odoo development guidelines states that the XML files defining the user interface should be
placed inside a views/ subdirectory.

Let's start creating the user interface for our To-Do application.

Adding menu items

Now that we have a model to store our data, we should make it available on the user interface.
For that, we should add a menu option to open the To-do Task model so that it can be used.

Create the views/todo_menu.xml file to define a menu item and the action performed by it:

```
<?xml version="1.0"?>
<odoo>
    <!-- Action to open To-do Task list -->
    <act_window id="action_todo_task" name="To-do Task" res_model="todo.task" view_mode="tree,form" />
    
    <!-- Menu item to open To-do Task list -->
    <menuitem id="menu_todo_task" name="Todos" action="action_todo_task" />
</odoo>
```

The user interface, including menu options and actions, is stored in database tables. The XML file is a
data file used to load those definitions into the database when the module is installed or upgraded.
The preceding code is an Odoo data file, describing two records to add to Odoo:

<li>The <act_window> element defines a client-side window action that will open the todo.task
model with the tree and form views enabled, in that order.</li>

<li>The <menuitem> defines a top menu item calling the action_todo_task action, which was
defined before.</li>
<p></p>
Both elements include an id attribute. This id attribute also called an XML ID , is very important: it
is used to uniquely identify each data element inside the module, and can be used by other elements toreference it. 
In this case, the <menuitem> element needs to reference the action to process, and needs
to make use of the <act_window> ID for that.

Our module does not yet know about the new XML data file. This is done by adding it to the data
attribute in the ```__manifest__.py``` file. It holds the list of files to be loaded by the module. Add this
attribute to the manifest's dictionary:

```'data': ['views/todo_menu.xml'],```

Now we need to upgrade the module again for these changes to take effect. Go to the Todos top menu
and you should see our new menu option available.

Even though we haven't defined our user interface view, clicking on the Todos menu will open an
automatically generated form for our model, allowing us to add and edit records.

Odoo is nice enough to automatically generate them so that we can start working with our model right
away.

So far, so good! Let's improve our user interface now.