
One of Odoo's most powerful feature is the ability to add features without directly modifying the
underlying objects.

This is achieved through inheritance mechanisms, functioning as modification layers on top of existing
objects. These modifications can happen at all levels: models, views, and business logic. Instead of
directly modifying an existing module, we create a new module to add the intended modifications.

<h2>Adding sharing capabilities to the To-Do app</h2>

Our To-Do application now allows users to privately manage their own to-do tasks. Won't it be great
to take the app to another level by adding collaboration and social networking features to it? We will
be able to share tasks and discuss them with other people.

We will do this with a new module to extend the previously created To-Do app and add these new
features using the inheritance mechanisms.

This will be our work plan for the feature extensions to be implemented:

<li>Extend the Task model, such as the user who is responsible for the task</li><br/>
<li>Modify the business logic to operate only on the current user's tasks, instead of all the tasks the
user is able to see</li><br/>
<li>Extend the views to add the necessary fields to the views</li><br/>
<li>Add social networking features: a message wall and the followers</li><br/>

We should add there a new ```todo_user``` directory for the module, containing an empty ```__init__.py``` file.

Now create ```todo_user/__manifest__.py``` , containing this code:
```
{
    'name': 'Multiuser To-Do',
    'description': 'Extend the To-Do app to multiuser.',
    'author': 'Daniel Reis','depends': ['todo_app'], 
}
```

We haven't done this here, but including the ```summary``` and ``category`` keys can be important when
publishing modules to the Odoo online app store.

Notice that we added the explicit dependency on todo_app module. This is necessary and important
for the inheritance mechanism to work properly. And from now on, when the todo_app module is
updated, all modules depending on it, such as todo_user module, will also be updated.

Next, install it. It should be enough to update the module list using the Update Apps List menu
option under Apps ; find the new module in the Apps list and click on its Install button.

Now, let's start adding new features to it


<h2>Extending models</h2>

New models are defined through Python classes. Extending them is also done through Python classes,
but with the help of an Odoo-specific inheritance mechanism.

To extend an existing model, we use a Python class with a ``_inherit`` attribute. This identifies the
model to be extended. The new class inherits all the features of the parent Odoo model, and we only
need to declare the modifications we want to introduce.

In fact, Odoo models exist outside our particular Python module, in a central registry. This registry,
can be accessed from model methods using ``self.env[<model name>]`` . For example, to get a
reference to the object representing the res.partner model, we would write
```self.env['res.partner']``` .

To modify an Odoo model, we get a reference to its registry class and then perform in-place changes
on it. This means that these modifications will also be available everywhere else where this new
model is used.

During the Odoo server startup, the module loading the sequence is relevant: modifications made by
one add-on module will only be visible to the add-on modules loaded afterward. So it's important for
the module dependencies to be correctly set, ensuring that the modules providing the models we use
are included in our dependency tree.

<h2>Adding fields to a model</h2>

We will extend the todo.task model to add a couple of fields to it: the user responsible for the task
and a deadline date.

The coding style guidelines recommended having a models/ subdirectory with one file per Odoo
model. So we should start by creating the model subdirectory, making it Python-importable.

Edit the ```todo_user/__init__.py``` file to have this content:

```from .import models```

Create ``todo_user/models/__init__.py`` with the following code:

``from . import todo_task``

The preceding line directs Python to look for a file called odoo_task.py in the same directory and
imports it. You would usually have a from line for each Python file in the directory:

Now create the ``todo_user/models/todo_task.py`` file to extend the original model:

```
from odoo import models, fields, api
class TodoTask(models.Model):
    _inherit = 'todo.task'
    user_id = fields.Many2one('res.users', 'Responsible')
    date_deadline = fields.Date('Deadline')
```

The class name ``TodoTask`` is local to this Python file and, in general, is irrelevant for other modules.
The ``_inherit`` class attribute is the key here: it tells Odoo that this class is inheriting and thus
modifying the todo.task model.

<h4>Note</h4>
Notice the _name attribute is absent. It is not needed because it is already inherited from the parent
model.

<h2>Modifying existing fields</h2>

As you can see, adding new fields to an existing model is quite straightforward. Since Odoo 8,
modifying the attributes on existing inherited fields is also possible. It's done by adding a field with
the same name and setting values only for the attributes to be changed.

For example, to add a help tooltip to the name field, we would add this line to ``todo_ task.py`` ,
described previously:

``name = fields.Char(help="What needs to be done?")``

This modifies the field with the specified attributes, leaving unmodified all the other attributes not
explicitly used here. If we upgrade the module, go to a to-do task form and pause the mouse pointer
over the Description field; the tooltip text will be displayed.


<h2>Modifying model methods</h2>

Inheritance also works at the business logic level. Adding new methods is simple: just declare their
functions inside the inheriting class.

To extend or change the existing logic, the corresponding method can be overridden by declaring a
method with the exact same name. The new method will replace the previous one, and it can also just
extend the code of the inherited class, using Python's super() method to call the parent method. It canthen add new logic around the original logic both before and after super() method is called.

For this, the original Clear All Done action is not appropriate for our task-sharing module anymore since it
clears all the tasks, regardless of their user. 

We need to modify it so that it clears only the current user
tasks. We will override (or replace) the original method with a new version that first finds the list
of completed tasks for the current user and then inactivates them:
```
@api.multi
def do_clear_done(self):
    domain = [('is_done', '=', True), '|', ('user_id', '=', self.env.uid), ('user_id', '=', False)]
    dones = self.search(domain)
    dones.write({'active': False})
    return True
```

We can improve the do_toggle_done() method so that it only performs its action on the tasks
assigned to the current user. This is the code to achieve that:
```
from odoo.exceptions import ValidationError
# ...
# class TodoTask(models.Model):
# ...
    @api.multi
    def do_toggle_done(self):
        for task in self:
            if task.user_id != self.env.user:
                raise ValidationError(
                'Only the responsible can do this!')
        return super(TodoTask, self).do_toggle_done()
```
The method in the inheriting class starts with a for loop to check that none of the tasks to toggle
belongs to another user. If these checks pass, it then goes on calling the parent class method, using
super() . If not an error is raised, and we should use for this the Odoo built-in exceptions. The most
relevant are ValidationError , used here, and UserError .

These are the basic techniques for overriding and extending business logic defined in model classes.
Next, we will see how to extend the user interface views.


<h2>Extending views</h2>

Forms, lists, and search views are defined using the arch XML structures. To extend views, we need
a way to modify this XML. This means locating XML elements and then introducing modifications at
those points.

Inherited views allow just that. An inherited view declaration looks like this:
```
<record id="view_form_todo_task_inherited" model="ir.ui.view">
    <field name="name">Todo Task form - User extension</field>
    <field name="model">todo.task</field>
    <field name="inherit_id" ref="todo_app.view_form_todo_task"/>
    <field name="arch" type="xml">
    <!-- ...match and extend elements here! ... -->
    </field>
</record>
```
The inherit_id field identifies the view to be extended by referring to its external identifier using
the special ref attribute.

Being XML, the best way to locate elements in XML is to use XPath expressions. For example, taking
the form view defined in the previous chapter, one XPath expression to locate the ```<field
name="is_done">``` element is ```//field[@name]='is_done'``` . This expression finds any ``field``
element with a ``name`` attribute that is equal to is_done .

Once the extension point is located, you can either modify it or have XML elements added near it. As
a practical example, to add the date_deadline field before the is_done field, we would write the
following in arch :
```
<xpath expr="//field[@name]='is_done'" position="before">
    <field name="date_deadline" />
</xpath>
```
Fortunately, Odoo provides shortcut notation for this, so most of the time we can avoid the XPath
syntax entirely. Instead of the preceding XPath element, we can just use information related to the type
of element type to locate and its distinctive attributes, and instead of the preceding XPath, we write
this:
```
<field name="is_done" position="before">
    <field name="date_deadline" />
</field>
```

The position attribute used with the locator element is optional and can have the following values:

<li>after: adds the content to the parent element, after the matched node.</li>

<li>before: adds the content, before the matched node.</li>
<li>inside: (default value) appended the content inside matched node.</li>
<li>replace: replaces the matched node. If used with empty content, it deletes
an element. Since Odoo 10 it also allows to wrap an element with other markup, by using $0 in the content to
represent the element being replaced.
<li>attributes: modifies the XML attributes of the matched element. This is done using in the
element content <attribute name="attr-name"> elements with the new attribute values to
set.</li>

For Example, in the Task form, we have the active field, but having it visible is not that useful. We
could hide it from the user. This can be done by setting its invisible attribute:
```
<field name="active" position="attributes">
    <attribute name="invisible">1</attribute>
</field>
```
Setting the invisible attribute to hide an element is a good alternative to using the replace locator
to remove nodes.


<h2>Extending the form view</h2>

Putting together all the previous form elements, we can add the new fields and hide the active field.
The complete inheritance view to extend the to-do tasks form is this:
```
<record id="view_form_todo_task_inherited" model="ir.ui.view">
    <field name="name">Todo Task form - User extension</field>
    <field name="model">todo.task</field>
    <field name="inherit_id" ref="todo_app.view_form_todo_task"/>
    <field name="arch" type="xml">
        <field name="name" position="after">
            <field name="user_id">
        </field>
        <field name="is_done" position="before">
            <field name="date_deadline" />
        </field>
        <field name="active" position="attributes">
            <attribute name="invisible">1</attribute>
        </field>
    </field>
</record>
```

This should be added to a views/todo_task.xml file in our module, inside the <odoo> element, as
shown in the previous module.

<h2>Extending the tree and search views</h2>

Tree and search view extensions are also defined using the arch XML structure, and they can be
extended in the same way as form views. We will continue our example by extending the list and
search views.

For the list view, we want to add the user field to it:
```
<record id="view_tree_todo_task_inherited" model="ir.ui.view">
    <field name="name">Todo Task tree - User extension</field>
    <field name="model">todo.task</field>
    <field name="inherit_id"ref="todo_app.view_tree_todo_task"/>
    <field name="arch" type="xml">
        <field name="name" position="after">
            <field name="user_id" />
        </field>
    </field>
</record>
```

For the search view, we will add the search by the user and predefined filters for the user's own tasks
and the tasks not assigned to anyone:
```
<record id="view_filter_todo_task_inherited" model="ir.ui.view">
    <field name="name">Todo Task tree - User extension</field>
    <field name="model">todo.task</field>
    <field name="inherit_id" ref="todo_app.view_filter_todo_task"/>
    <field name="arch" type="xml">
        <field name="name" position="after">
            <field name="user_id" />
            <filter name="filter_my_tasks" string="My Tasks" domain="[('user_id','in',[uid,False])]" />
            <filter name="filter_not_assigned" string="Not Assigned" domain="[('user_id','=',False)]" />
        </field>
    </field>
</record>
```

<h2>Adding the social network features</h2>

The social network module (technical name mail ) provides the message board found at the bottom of
many forms and the Followers feature, as well as the logic regarding messages and notifications. This
is something we will often want to add to our models, so let's learn how to do it.

The social network messaging features are provided by the mail.thread model of the mail module.
To add it to a custom model, we need to do the following:

<li>Have the module depend on mail</li>
<li>Have the class inherit from mail.thread</li>
<li>Have the followers and thread widgets added to the form view</li>
<li>Optionally, we need to set up record rules for followers.</li><br/>

Let's follow this checklist.

Regarding the first point, our extension module will need the additional mail dependency on the
module ``__manifest__.py`` manifest file:

```'depends': ['todo_app', 'mail'],```

Regarding the second point, the inheritance on mail.thread is done using the _inherit attribute we
used before. But our to-do task extension class is already using the _inherit attribute. Fortunately, it
can accept a list of models to inherit from, so we can use this to make it also include the inheritance
on mail.thread :
```
_name = 'todo.task'
_inherit = ['todo.task', 'mail.thread']
```
The mail.thread is an abstract model. Abstract models are just like regular models, except that
they don't have a database representation; no actual tables are created for them. Abstract models are
not meant to be used directly. Instead, they are expected to be used as mixin classes, as we just did.
We can think of them as templates with ready-to-use features. To create an abstract class, we just need
it to use models.AbstractModel instead of models.Model for the class defining them.

For the third point, we want to add the social network widgets at the bottom of the form. This is done
by extending the form view definition. We can reuse the inherited view we already created,
view_form_todo_task_inherited , and add this to its arch data:
```
<sheet position="after">
    <div class="oe_chatter">
        <field name="message_follower_ids" widget="mail_followers" />
        <field name="message_ids" widget="mail_thread" />
    </div>
</sheet>
```

The final step, that is step four, is to set up record rules for followers: row-level access control. This
is only needed if our model is required to limit other users from accessing the records. In this case,
we want each to-do task record to also be visible to any of its followers.

We already have a Record Rules defined on the to-do task model, so we need to modify it to add this
new requirement. That's one of the things we will be doing in the next section