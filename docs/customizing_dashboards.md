# Customizing Dashboards

In order to customize which attributes get displayed for each resource,
edit the dashboard file generated by the installation generator.

By default, the file will look something like this:

```ruby
require "administrate/dashboard/base"

class CustomerDashboard < Administrate::Dashboard::Base
  ATTRIBUTE_TYPES = {
    id: Field::Integer,
    name: Field::String,
    email: Field::String,
    created_at: Field::DateTime,
    updated_at: Field::DateTime,
    orders: Field::HasMany,
  }

  COLLECTION_ATTRIBUTES = [
    :id,
    :name,
    :email,
    :created_at,
    :updated_at,
    :orders,
  ]

  SHOW_PAGE_ATTRIBUTES = [
    :id,
    :name,
    :email,
    :created_at,
    :updated_at,
    :orders,
  ]

  FORM_ATTRIBUTES = [
    :name,
    :email,
    :orders,
  ]
end
```

To change which attributes appear on each of the `index`, `show`, and `edit`
pages, add or remove attributes to each constant array.

Finally, the `ATTRIBUTE_TYPES` method defines how each attribute is displayed
throughout the dashboard. There are a number of `Field` classes that you can
specify, including:

- `Field::BelongsTo`
- `Field::Boolean`
- `Field::DateTime`
- `Field::Email`
- `Field::HasMany`
- `Field::HasOne`
- `Field::Image`
- `Field::Number`
- `Field::Polymorphic`
- `Field::String`

Each of the `Field` types take a different set of options,
which are specified through the `.with_options` class method.
For example, you might use the following to display currency,
if the value is stored by the number of cents:

```ruby
  unit_price_in_cents: Field::Number.with_options(
    title: "Unit Price",
    prefix: "$",
    multiplier: 0.01,
    decimals: 2,
  )
```

[define your own]: /adding_custom_field_types
