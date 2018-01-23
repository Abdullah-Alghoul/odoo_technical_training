<h4>F3. Creating the form view</h4>

All views are stored in the database, in the ```ir.ui.view``` model. To add a view to a module, we
declare a ```<record>``` element describing the view in an XML file, which is to be loaded into the
database when the module is installed.

Add this new ```views/todo_view.xml``` file to define our form view:

```
<?xml version="1.0"?>
<odoo>
    <record id="view_form_todo_task" model="ir.ui.view">
        <field name="name">To-do Task Form</field>
        <field name="model">todo.task</field>
        <field name="arch" type="xml">
            <form string="To-do Task">
                <group>
                    <field name="name"/>
                    <field name="is_done"/>
                    <field name="active" readonly="1"/>
                </group>
            </form>
        </field>
    </record>
</odoo>
```
Remember to add this new file to the data key in the manifest file, otherwise, our module won't know
about it and it won't be loaded.

This will add a record to the ```ir.ui.view``` model with the identifier **view_form_todo_task**. The
view is for the ```todo.task``` model and is named To-do Task Form .

The most important attribute is arch , and it contains the view definition, highlighted in the XML code
above. The ```<form>``` tag defines the view type, and in this case, contains three fields.

Form contains two elements: ```<header>``` to contain action buttons and ```<sheet>``` to contain the data fields.

We can now replace the basic ```<form>``` defined in the previous section with this one:

```
<form>
    <header>
        <!-- Buttons go here-->
    </header>
    <sheet>
        <!-- Content goes here: -->
        <group>
            <field name="name"/>
            <field name="is_done"/>
            <field name="active" readonly="1"/>
        </group>
    </sheet>
</form>
```

<h4>F4. Adding action buttons</h4>

Forms can have buttons to perform actions. These buttons are able to run window actions such as
opening another form or run Python functions defined in the model.

They can be placed anywhere inside a form, but for document-style forms, the recommended place for
them is the ```<header>``` section.

For our application, we will add two buttons to run the methods of the ```todo.task``` model:
```
<header>
    <button name="do_toggle_done" type="object"
    string="Toggle Done" class="oe_highlight" />
    <button name="do_clear_done" type="object"
    string="Clear All Done" />
</header>
```
The basic attributes of a button comprise the following:

<li>string with the text to display on the button</li>
<li>type of action it performs</li>
<li>name is the identifier for that action</li>
<li>class is an optional attribute to apply CSS styles, like in regular HTML</li>

<h4>F5. Using groups to organize forms</h4>

The ```<group>``` tag allows you to organize the form content. Placing ```<group>``` elements inside a
```<group>``` element creates a two column layout inside the outer group. Group elements are advised to
have a name attribute so that its easier for other modules to extend them.

We will use this to better organize our content. Let's change the <sheet> content of our form to match
this:
```
<sheet>
    <group name="group_top">
        <group name="group_left">
            <field name="name"/>
        </group>
        <group name="group_right"><field name="is_done"/>
            <field name="active" readonly="1"/>
        </group>
    </group>
</sheet>
```
At this point, our ```todo.task``` form view should look like this:
```
<form>
    <header>
        <button name="do_toggle_done" type="object"
        string="Toggle Done" class="oe_highlight" />
        <button name="do_clear_done" type="object"
        string="Set Inactive" />
    </header>
    <sheet>
        <group name="group_top">
            <group name="group_left">
                <field name="name"/>
            </group>
            <group name="group_right">
                <field name="is_done"/>
                <field name="active" readonly="1" />
            </group>
        </group>
    </sheet>
</form>
```

**Tip**

Remember that, for the changes to be loaded to our Odoo database, a module upgrade is needed. To
see the changes in the web client, the form needs to be reloaded: either click again on the menu option
that opens it or reload the browser page ( F5 in most browsers).

The action buttons won't work yet since we still need to add their business logic.

<h4>F6. Adding list and search views</h4>

When viewing a model in list mode, a ```<tree>``` view is used. Tree views are capable of displaying
lines organized in hierarchies, but most of the time, they are used to display plain lists.

We can add the following tree view definition to ``todo_view.xml`` :
```
<record id="view_tree_todo_task" model="ir.ui.view">
    <field name="name">To-do Task Tree</field>
    <field name="model">todo.task</field>
    <field name="arch" type="xml">
        <tree>
            <field name="name"/>
            <field name="is_done"/>
        </tree>
    </field>
</record>
```

This defines a list with only two columns: name and is_done . We also added a nice touch: the lines
for done tasks **(is_done==True)** are shown grayed out.

At the top-right corner of the list, Odoo displays a search box. The fields it searches in and the
available filters are defined by a ```<search>``` view.

As before, we will add this to ```todo_view.xml``` :
```
<record id="view_filter_todo_task" model="ir.ui.view">
    <field name="name">To-do Task Filter</field>
    <field name="model">todo.task</field>
    <field name="arch" type="xml">
        <search>
            <field name="name"/>
            <filter string="Not Done" domain="[('is_done','=',False)]"/>
            <filter string="Done" domain="[('is_done','!=',False)]"/>
        </search>
    </field>
</record>
```
The ```<field>``` elements define fields that are also searched when typing in the search box. The
```<filter>``` elements add predefined filter conditions, that can be toggled with a user click, defined
using a specific syntax.

<h4>F7. Adding business logic</h4>

We should edit the ```todo_model.py``` Python file to add to the class the methods called by the buttons.
First, we need to import the new API, so add it to the import statement at the top of the Python file:

```from odoo import models, fields, api```

The action of the **Toggle Done** button will be very simple: just toggle the **Is Done?** flag. For logic on
records, use the ```@api.multi``` decorator. Here, self will represent a recordset, and we should then
loop through each record.

Inside the TodoTask class, add this:

```
@api.multi
def do_toggle_done(self):
    for task in self:
        task.is_done = not task.is_done
    return True
```

The code loops through all the to-do task records and, for each one, modifies the is_done field,
inverting its value.

For the **Clear All Done** button, we want to go a little further. It should look for all active records that
are done, and make them inactive. Usually form buttons are expected to act only on the selected
record, but in this case, we will want it also act on records other than the current one:
```
@api.multi
def do_clear_done(self):
    if self.is_done is True:
        self.write({'active': False})
    return True
```
On methods decorated with ```@api.model```, the self variable represents the model with no record in
particular. We will build a ``dones`` recordset containing all the tasks that are marked as done. Then, we
set the ``active`` flag to ``False`` on them.

The ```search``` method is an API method that returns the records that meet some conditions. These
conditions are written in a domain, which is a list of triplets.

The ```write``` method sets the values at once on all the elements of the recordset. The values to write are
described using a dictionary. Using write here is more efficient than iterating through the recordset to
assign the value to each of them one by one.

<h4>F8. Adding access control security</h4>

You might have noticed that, upon loading, our module is getting a warning message in the server log:

The model todo.task has no access rules, consider adding one.

The message is pretty clear: our new model has no access rules, so it can't be used by anyone other
than the admin superuser. As a superuser, the admin ignores data access rules, and that's why we
were able to use the form without errors. But we must fix this before other users can use our model

This information has to be provided by the module using a data file to load the lines into the
```ir.model.access model```.

This is done using a CSV file named security/ir.model.access.csv . Let's add it with the
following content:
```
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
acess_todo_task_group_user,todo.task.user,model_todo_task,base.group_user,1,1,1,1
```

The filename corresponds to the model to load the data into, and the first line of the file has the
column names. These are the columns provided in our CSV file:

<li>id is the record external identifier (also known as XML ID). It should be unique in our module.</li><br/>

<li>name is a description title. It is only informative and it's best if it's kept unique. Official
modules usually use a dot-separated string with the model name and the group. Following this
convention, we used ```todo.task.user``` .</li><br/>

<li>model_id is the external identifier for the model we are giving access to. Models have XML
IDs automatically generated by the ORM: for todo.task , the identifier is model_todo_task .</li><br/>

<li>group_id identifies the security group to give permissions to. The most important ones are
provided by the base module. The Employee group is such a case and has the identifier
base.group_user .</li><br/>

<li>perm fields flag the access to grant read , write , create , or unlink (delete) access.</li><br/>

We must not forget to add the reference to this new file in the __manifest__.py descriptor's data
attribute. It should look like this:
```
'data': [
    'security/ir.model.access.csv',
    'views/todo_view.xml',
    'views/todo_menu.xml',
],
```
As before, upgrade the module for these additions to take effect. The warning message should be
gone, and we can confirm that the permissions are OK by logging in with the user demo (password is
also demo ).