<h2>Understanding Model Relationships</h2>

<h4>Many2one Relationship</h4>

The Many2one relationship accepts two positional arguments: the related model (corresponding to the
comodel keyword argument) and the title string . It creates a field in the database table with a
foreign key to the related table.

<h4>Many-to-many relationships</h4>

The Many2many minimal signature accepts one argument for the related model, and it is recommended
to also provide the string argument with the field title.

At the database level, it does not add any columns to the existing tables. Instead, it automatically
creates a new relationship table that has only two ID fields with the foreign keys for the related
tables. The relationship table name and the field names are automatically generated. The relationship
table name is the two table names joined with an underscore with _rel appended to it.

On some occasions we may need to override these automatic defaults.

One such case is when the related models have long names, and the name for the automatically
generated relationship table is too long, exceeding the 63 characters PostgreSQL limit. In these cases
we need to manually choose a name for the relationship table, to conform to the table name size limit.

Another case is when we need a second many-to-many relationship between the same models. In
these cases we need to manually provide a name for the relationship table, so that it doesn't collide
with the table name already being used for the first relationship.

<h4>One-to-many inverse relationships</h4>

An inverse of a Many2one can be added to the other end of the relationship. This has no impact on the
actual database structure, but allows us easily browse from the one side of the many related records.
A typical use case is the relationship between a document header and its lines.

In our example, a One2many inverse relationship on Stages allows us to easily list all the Tasks in that
Stage

<h2>Computed fields</h2>

Fields can have values calculated by a function, instead of simply reading a database stored value. A
computed field is declared just like a regular field, but has the additional compute argument defining
the function used to calculate it.

The ```@api.depends``` decorator is needed when the computation depends on other fields, as it usually
does. It lets the server know when to recompute stored or cached values. One or more field names are
accepted as arguments and dot-notation can be used to follow field relationships.

<h2>Related fields</h2>

The computed field we implemented in the previous section just copies a value from a related record
into a model's own field. However this is a common usage that can be automatically handled by
Odoo.

The same effect can be achieved using related fields. They make available, directly on a model,
fields that belong to a related model, accessible using a dot-notation chain. This makes them usable in
situations where dot-notation can't be used, such as UI form views.

To create a related field, we declare a field of the needed type, just like with regular computed fields,
but instead of compute we use the related attribute with the dot-notation field chain to reach the
desired field.

<h2>Model Constraints<h2>

To enforce data integrity, models also support two types of constraints: SQL and Python
SQL constraints are added to the database table definition and are enforced directly by PostgreSQL.

They are defined using the _sql_constraints class attribute. It is a list of tuples with: the constraint
identifier name; the SQL for the constraint; and the error message to use.

A common use case is to add unique constraints to models. Suppose we don't want to allow two
active tasks with the same title:
```
# class TodoTask(models.Model):
    _sql_constraints = [
    ('todo_task_name_uniq',
    'UNIQUE (name, active)',
    'Task title must be unique!')]
```
Python constraints can use a piece of arbitrary code to check the conditions. The checking function
should be decorated with @api.constraints , indicating the list of fields involved in the check. The
validation is triggered when any of them is modified and will raise an exception if the condition fails.

For example, to validate that a Task name is at least five characters long, we could add the following
constraint:

```
from odoo.exceptions import ValidationError
# class TodoTask(models.Model):
@api.constrains('name')
def _check_name_size(self):
    for todo in self:
        if len(todo.name) < 5:
        raise ValidationError('Must have 5 chars!')
```