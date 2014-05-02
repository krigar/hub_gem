spree_hub
========


Installation
------------

Add spree_hub to your Gemfile:

```ruby
gem 'spree_hub', github: 'spree/hub_gem', branch: '2-2-stable'
```

Bundle your dependencies:

```shell
bundle
```

Add the hub credentials to `config/initializers/spree.rb`:

```ruby
Spree::Hub::Config[:hub_token] = "sdfsfddfdss"
Spree::Hub::Config[:enable_push] = true
```

If given a Push URL, you may need to set the following:
```ruby
Spree::Hub::Config[:hub_push_uri] = "new url"
```

To enable auto pushing of objects make sure the following configuration option is set
```ruby
Spree::Hub::Config[:enable_auto_push] = true
```

Testing
-------

First bundle your dependencies, then run `rake`. `rake` will default to building the dummy app if it does not exist, then it will run specs. The dummy app can be regenerated by using `rake test_app`.

```shell
bundle
bundle exec rake
```

When testing your applications integration with this extension you may use it's factories.
Simply add this require statement to your spec_helper:

```ruby
require 'spree_hub/factories'
```


Consuming webhooks from the hub
-------------------------------

This extension provides your store with a generic endpoint to receive any webhook called
from the hub. The format for all of those is: `http://mystore.com/hub/<WEBHOOK>`

So for the add_product webhook, the endpoint url is `http://mystore.com/hub/add_product`

You need to implement the webhook handler yourself, since no store is a like.
The convention with this extension is that we dynamicly initialize a handler based on the webhook.
So with the `add_product` sample, we will initialize `Spree::Hub::Handler::AddProductHandler` and call `process`

Make sure you inherit your handler from `Spree::Hub::Handler::Base`


Copyright (c) 2014 Spree Commerce, Inc. and other contributors, released under the New BSD License
