# announcements

## Quick start

1. Requirements: rails >= 3.1.0 and jquery
2. Add `gem 'announcements'` to your Gemfile and run `bundle`
3. Run `rails g announcements:install`
4. Use `<%= announce Announcement.newest %>` in your views to display the latest announcement
5. Create your first announcement in `rails c` by simply creating a new Announcement record, like `Announcement.create(:body => 'This is my first announcement!')`
6. Next, add some CSS (find an example below; the default output is quite plain and ugly) and customise it.

## Styling

By default, the announcement text and hide message text are wrapped in a div called "info" (if you want to customise that, see the Customisation section below).
You can use the following css in your application.css file to start:

```css
.info {
	background: #D5EDF8;
	color: #205791;
	padding: 0.8em;
	margin-bottom: 1em;
	border: 2px solid #92CAE4;
}

.hide_announcement {
	cursor: pointer;
	float: right;
}
```

## Customisation

The default HTML output of the `announce` helper is

```html
<div class="info">
	My announcement!
	<span class="hide_announcement" data-announcementid="1">hide message</span>
</div>
```

The default div class is `info`. You can specify you own like that:

```ruby
<%= announce Announcement.newest, :div_class => "mydiv" %>
```

You can also change the "hide message" text:

```ruby
<%= announce Announcement.newest, :div_class => "mydiv", :hide_message => "X" %>
```

## How it works

The gem creates an Announcement model with a few class methods like `Announcement.newest`. The Announcement model has a body:text (the actual announcement text) 
and a type:string (which you can use for different types of announcements, e.g. public (everyone) and private (only for registered users)). There is also a js file in vendor/assets/javascripts
which permanently hides the announcement by creating a cookie (that's when you click on the 'hide message' text).

## How to uninstall

There is no uninstaller at this point, but you can simply remove the following files manually:

1. app/models/announcement.rb
2. vendor/assets/javascripts/announcements.js

You also have to remove the `//= require announcements` line in your app/assets/javascripts/application.js file, and rollback the `create_announcements` migration.