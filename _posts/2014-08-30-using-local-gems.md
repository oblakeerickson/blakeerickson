---
layout: post
title: Using Local Gems
---

Today I started working on adding some features to the [discourse_api](), but I needed to work on the gem locally and rebuild it to test my changes. Using a gem locally took me a lot longer than I wanted to spend today, so I thought I'd write up how to do it.

First of all I would delete the gem that you might have installed from ruby gems already:

{% raw %}
    gem uninstall discourse_api
{% endraw %}

Then clone a copy of the gem

{% raw %}
    git clone https://github.com/discourse/discourse_api.git
{% endraw %}

Create a project folder for you new app

{% raw %}
    mkdir app
{% endraw %}

Inside of our `app` directory create a `Gemfile` with the contents:

{% raw %}
    source 'https://rubygems.org'
    gem 'discourse_api', :path => '/full/path/to/discourse_api'
{% endraw %}

As you can see we specified a `:path` pointing to where the gem can be found locally. Now type:

{% raw %}
    bundle install
{% endraw %}

Once of the lines of output fromt the `bundle install` command will be:

{% raw %}
    Using discourse_api 0.2.1 from source at /vagrant/discourse_api
{% endraw %}

This way you can tell it grabbed a local version of them gem and not one from rubygems.org.

Now create a file called `app.rb` with the contents:

{% highlight ruby %}
require "discourse_api"

client = DiscourseApi::Client.new("https://meta.discourse.org")
puts client.user('oblakeerickson')
{% endhighlight %}

Now to run it you need to type `bundle exec ruby app.rb` instead of just `ruby app.rb`:

{% raw %}
    bundle exec ruby app.rb
{% endraw %}

Hopefully remembering to specify a `:path` and to use `bundle exec` will make using a gem locally much easier for you.
