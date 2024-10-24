---
layout: post
date: 2020-10-21
title: slim setup
---

My slim setup is faily simple. 

The first important bit is to tell sinatra to set slim as the engine used to generate partials.

```ruby
set :partial_template_engine, :slim
```
Then I define some special shorcuts for the most repetitive declarations:
  
- '&' to denote an input field
- '#' to denote the id
- '.' to denote the class

```ruby
Slim::Engine.set_options shortcut: {
  '&' => {tag: 'input', attr: 'type'}, 
  '#' => {attr: 'id'}, 
  '.' => {attr: 'class'}
  '@' => {attr: %w(id name)}
  }
```
The most peculiar shortcut is the @ which sets both the `id` and the `name` attributes at the same time.

For example, a typical text input field with its label will look like.

```slim
label for="name" name
&text@name.u-full-width[
  required
  data-action="input->form-validator#validate" 
  value=@object&.name]
```
Note the safe call of `value=@object&.name`. In case `@object` is `nil`, the value will not be defined but no 
exeption will be thrown.

## Form Declaration

```slim
.container.screen-box.medium-form data-controller="form" 

  form[
    action="/person/#{(@object.nil? ? "new" : @object.id)}" 
    method="POST"
    data-controller="form-validator"
    data-form-target="form"
    data-action="keydown.ctrl+enter@window->form#enter \
      keydown.esc@window->form#escape"]
```