jquery-ujs-extended
===================

Extend usage of html5 data attributes of the jquery UJS gem in the context of Ajax calls. 
It's just global attributes listeners I find myself often needing to rewrite in my new projects to save time on javascript writing. I extracted it as a gem.

#Prerequisites

This has been tested on Rails 3.2.8 so far. Since it's just a collection of JS listeners, it should work on any version really.

Requires :
- Usage of asset pipeline
- Coffeescript
- jquery-rails

#Installation

Before it's released as a gem, you can open your Gemfile and in the asset group add :

    gem 'jquery_ujs_extended', git: https://github.com/anthonyalberto/jquery-ujs-extended

#Usage

When specifying a target DOM element in custom data attributes, you have to use the [jQuery selector](http://api.jquery.com/category/selectors/) syntax. You can modify several elements on the DOM at once this way

##Ajax listeners

This applies to <form> and <a> elements. Needs to be used with `data-remote` from jquery-ujs

* data-update listener that automatically updates the DOM elements
       link_to "Update", url_path, data: {remote: true, update: "#div1"}
       form_for @object, data: {remote: true, update: "#div1"}
* data-destroy listener that automatically deletes the DOM elements
       link_to "Destroy", url_path, data: {remote: true, destroy: ".class1"}
       form_for @object, data: {remote: true, destroy: ".class1 .class2"}
* data-append listener that automatically appends to the DOM elements
       link_to "Append", url_path, data: {remote: true, append: "#div1 span .class1"}
* data-loader. Takes a DOM element. Will show the DOM element before sending the request, and hide it when the request is completed. This is best used to show a spinner image during a request.
       <%= link_to "Loader", url_path, data: {remote: true, append: ".loader"} %>
       <%= image_tag "/my/image.jpg", style: {display:'none'}, class: 'loader' %>
* data-redirect. Takes a url. Redirects to the url on ajax success.
       link_to "redirect", url_path, data: {remote: true, redirect: "/my/url"}

##Ajax requests

* data-url. Applies to form inputs. Calls the url whenever the field has changed. 
Compatible with data- methods above. Specify a data-attribute containing the name of the attribute to send to the server, otherwise will use the 'name' of the field.
       <%= select_tag "country", options_for_select_from_collection(Country.all), data:{url:'/my/ajax_url', update:'#state_select', type: 'html'}

For all the above, DOM elements should be passed like this :
* ID : `data: {update: '#dom_id'}`
* Class : `data: {update: '.dom_class'}`
* Chaining : `data: {update: '#dom_id #dom_id2 .dom_class'}`

##Behaviour

* data-integer. If specified and applied to a text field, will prevent the field from being anything but an integer.Value: minimum value. Leave blank if you don't want one.
    text_field_tag "quantity", 1, data: {integer: 1}
* data-float. If specified and applied to a text field, will prevent the field from being anything but a float.Value: minimum value. Leave blank if you don't want one.
    text_field_tag "price", 1, data: {float: 0.01}


#Bugs? Thoughts? Ideas to make it better?

Don't hesitate to open an issue here and I'll what I can do!
