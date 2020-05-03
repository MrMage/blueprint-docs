---
title: Model Keys and Indexes
description: Description
extends: _layouts.documentation
section: content
---
## Model Keys and Indexes
Blueprint supports defining keys and indexes on your models through the column definition and by convention.

Within the column definition, you may specify a key or index using the `id` column type or the `foreign`, `index`, or `unique` column modifiers.

The simplest of these are the `index` and `unique` modifiers. Blueprint will generate the necessary code to the migration to add the _index_. In turn, Laravel will create an index for this column.

The `foreign` column modifier will also generate the necessary code to create an index on the column. In addition, it will generate code to add the reference and cascade "on delete" constraints.

By default, Blueprint will automatically infer the foreign reference from the column name just as Laravel does. For example, a column name of `user_id`, would imply a reference to the `id` column of the `users` table.

If you are not following Laravel's naming conventions, you may set the attribute on the `foreign` modifier. Blueprint supports either the foreign table name or the table and column name using dot notation.

For example, all of the following column definitions generate a foreign reference to the `id` column of the `users` table.

```yaml
    user_id: id foreign
    owner_id: id foreign:users
    uid: id foreign:users.id
```

Finally, while the `id` column type does not create an explicit index on the database, it does imply a foreign key relationships for the model.

Similar to the `foreign` column modifier, you may specify an attribute on the `id` column type. In this case, you specify the foreign model name or the model and column name using dot notation.

^^^
**When to use `foreign`?**
It is only necessary to specify `foreign` when you want the constraints. Otherwise, `id` alone is all that is necessary to create the appropriate relationships between your models.

If you always want the constraints, you should take a look at the `use_constraints` option in the [advanced configuration](/docs/advanced-configuration).
^^^