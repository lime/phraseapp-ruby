# phraseapp-ruby

phraseapp-ruby is a Ruby gem that allows you to interact with the [PhraseApp API](http://docs.phraseapp.com/api/v2/).

PhraseApp is a translation management platform for software projects. You can collaborate on language file translation with your team or order translations through our platform. The API allows you to import locale files, download locale files, tag keys or interact in other ways with the localization data stored in PhraseApp for your account.

phraseapp-ruby is not a replacement for the **phrase gem**, it is a pure API client for programmaticly using our features inside your own applications and does not support the push or pull commands for locale files. However, it does support uploading and downloading of single locale files through the according API endpoints.

If you're looking for a CLI sync command for PhraseApp, please user our official [PhraseApp client](http://docs.phraseapp.com/guides/working-with-phraseapp/command-line-client). The **phrase gem** is deprecated and will be discontinued at the end of 2015.

## Installation

Install the gem:

    gem install phraseapp-ruby

or add it to your Gemfile when using bundler:

    gem 'phraseapp-ruby'

and install it via

    bundle install

## Usage

Setup an [Access Token in your PhraseApp user profile](https://phraseapp.com/settings/oauth_access_tokens) for Authentication.

```ruby
# Require the gem
require 'phraseapp-ruby'

# Setup Authentication Credentials and Client
credentials = PhraseApp::Auth::Credentials.new(token: "YOUR_ACCESS_TOKEN")
client = PhraseApp::Client.new(credentials)

# List projects page 1 and list 10 projects per_page
rsp, err = client.projects_list(1, 10)
puts rsp

# Create a new key
params = PhraseApp::RequestParams::TranslationKeyParams.new(name: "foo")
rsp, err = client.key_create('YOUR_PROJECT_ID', params)
puts rsp
```

There are also other ways of authentication, which are described in our [API v2 Documentation](http://docs.phraseapp.com/api/v2/)

## Documentation

For a full list of available client actions, see the [phraseapp-ruby Documentation](http://www.rubydoc.info/gems/phraseapp-ruby/PhraseApp/Client)

The actions are generated automatically from our API specification, so once you get the hang of the Ruby specific naming, you should be able to infer names of actions and endpoints through our [API v2 Documentation](http://docs.phraseapp.com/api/v2/)

## OpenSSL

Please note that outdated certificates or old versions of OpenSSL may cause connection issues, especially on Mac OSX. We recommend using Ruby 2.2.2 with OpenSSL 1.0.2d or later. If you experience OpenSSL-related errors, try the following.

Upgrade OpenSSL using Homebrew:

```shell
$ brew upgrade openssl
$ brew install openssl
```

If you are using RVM, also run:

```shell
$ rvm osx-ssl-certs status all
$ rvm osx-ssl-certs update all
````

As a workaround, you can disable certificate verification in the Credentials:

```ruby
credentials = PhraseApp::Auth::Credentials.new(token: "YOUR_ACCESS_TOKEN", skip_ssl_verification: true)
client = PhraseApp::Client.new(credentials)
```

This is **not recommended** and should only be used as a temporary workaround.

## Contributing 

This library is auto-generated from templates that run against a API specification file. Therefore we can not accept any pull requests in this repository. Please use the [GitHub Issue Tracker](https://github.com/phrase/phraseapp-ruby/issues) to report bugs.


## Further reading

* [phraseapp-ruby documentation](http://www.rubydoc.info/gems/phraseapp-ruby)
* [PhraseApp](https://phraseapp.com)
* [PhraseApp API documentation](http://docs.phraseapp.com/api/v2/)
