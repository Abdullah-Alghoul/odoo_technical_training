<h1>A. Introduction to Odoo module</h1>

Both server and client extensions are packaged as modules which are optionally loaded in a database.

Odoo modules can either add brand new business logic to an Odoo system, or alter and extend existing business logic: a module can be created to add your country's accounting rules to Odoo's generic accounting support, while the next module adds support for real-time visualisation of a bus fleet.

Everything in Odoo thus starts and ends with modules.

<h1>B. Composition of a module</h1>
An Odoo module can contain a number of elements:
<h4>Business objects</h4>
    Declared as Python classes, these resources are automatically persisted by Odoo based on their configuration
<h4>Data files</h4>
    XML or CSV files declaring metadata (views or reports), configuration data (modules parameterization), demonstration data and more
<h4>Web controllers</h4>
    Handle requests from web browsers
<h4>Static web data</h4>
    Images, CSS or javascript files used by the web interface or website
    
<h1>C.Module structure</h1>

Each module is a directory within a module directory. Module directories are specified by using the ```--addons-path``` option.

most command-line options can also be set using a configuration file

An Odoo module is declared by its manifest.

A module is also a Python package with a ```__init__.py``` file, containing import instructions for various Python files in the module.

For instance, if the module has a single ```mymodule.py``` file ```__init__.py``` might contain:

```from . import mymodule```

Every module has the following structure:

<span>1. init File</span>

```__init__.py```

```
# -*- coding: utf-8 -*-
from . import controllers
from . import models
```

<span>2. Manifest File</span>

```openacademy/__manifest__.py```

```
# -*- coding: utf-8 -*-

{
    'name': "To-Do Application",

    'summary': """Manage trainings""",

    'description': """
        Open Academy module for managing trainings:
    """,

    'author': "My Company",
    'website': "http://www.yourcompany.com",

    # any module necessary for this one to work correctly
    'depends': ['base'],

    # always loaded
    'data': [
        # 'security/ir.model.access.csv',
        'templates.xml',
    ],
}

```
<span>3. Models</span>

```models.py```

```
# -*- coding: utf-8 -*-

from odoo import models, fields, api

# class openacademy(models.Model):
#     _name = 'openacademy.openacademy'

#     name = fields.Char()

```

<span>4. Views</span>

```templates.xml```

```
<odoo>

        <!-- <template id="listing"> -->
        <!--   <ul> -->
        <!--     <li t-foreach="objects" t-as="object"> -->
        <!--       <a t-attf-href="{{ root }}/objects/{{ object.id }}"> -->
        <!--         <t t-esc="object.display_name"/> -->
        <!--       </a> -->
        <!--     </li> -->
        <!--   </ul> -->
        <!-- </template> -->
        <!-- <template id="object"> -->
        <!--   <h1><t t-esc="object.display_name"/></h1> -->
        <!--   <dl> -->
        <!--     <t t-foreach="object._fields" t-as="field"> -->
        <!--       <dt><t t-esc="field"/></dt> -->
        <!--       <dd><t t-esc="object[field]"/></dd> -->
        <!--     </t> -->
        <!--   </dl> -->
        <!-- </template> -->

</odoo>

```

<span>5. Access Writes/Security</span>

```security/ir.model.access.csv```

```
id,name,model_id/id,group_id/id,perm_read,perm_write,perm_create,perm_unlink
access_openacademy_openacademy,openacademy.openacademy,model_openacademy_openacademy,,1,0,0,0```

