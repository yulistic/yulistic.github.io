---
author: yulistic
comments: true
date: 2016-05-12 06:49:07+00:00
layout: post
link: http://yulistic.com/?p=289
slug: install-gollum-wiki-on-centos-6-5
title: Install Gollum wiki on CentOS 6.5
wordpress_id: 289
language:
- English
tags:
- centos
- gollum
- linux
- ruby
- rugged
- rvm
- wiki
topics:
- Linux
- Problems &amp; Solutions
---

# Intro.


I decided to use [gollum](https://github.com/gollum/gollum/wiki) wiki, because of following reasons.



	
  * Bitbucket wiki supports poor searching functionality.

	
  * Gollum gives us a nice view and a convenient navigating functionality.

	
  * Gollum is easy to install, and light-weight.

	
  * Gollum supports pure markdown language.


I tried to install gollum in two different system: Ubuntu 14.04 and CentOS 6.5. There was no special problem when installing in Ubuntu, but there were in CentOS.


# Basic installation




## rvm


_rvm_ is [Ruby Version Manager](https://rvm.io/) that is a ruby manager maintained by third party. Because _yum_ in CentOS 6.5 supports only 1.8.x version _ruby_, we need another way to install higher version of _ruby_. Basically, you can follow the instructions mentioned on the _rvm_ hompage.



	
  1. Get key.

    
    # gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    




	
  2.  Install _rvm_.

    
    # curl -sSL https://get.rvm.io | bash -s stable







## ruby (2.2.1)


_ruby_ will be installed with RVM.

Check the _ruby_ installation with command: `gem`.

    
    # gem
    RubyGems is a sophisticated package manager for Ruby.  This is a
    basic help message containing pointers to more information.
    
      Usage:
        gem -h/--help
        gem -v/--version
        gem command [arguments...] [options...]
    
      Examples:
        gem install rake
        gem list --local
        gem build package.gemspec
        gem help install
    
      Further help:
        gem help commands            list all 'gem' commands
        gem help examples            show some examples of usage
        gem help platforms           show information about platforms
        gem help <COMMAND>           show help on COMMAND
                                       (e.g. 'gem help install')
        gem server                   present a web page at
                                     http://localhost:8808/
                                     with info about installed gems
      Further information:
        http://rubygems.rubyforge.org




## gollum


Install _gollum_. If you need to be root, use sudo.

    
    [sudo] gem install gollum




# Usage


If you already have a wiki in your github or bitbucket project, clone it into your local machine.

    
    # git clone [your remote git repository address]


If not, make a new git project.

    
    # mkdir proj
    # cd proj
    # git init


In root directory of your git project, just `gollum`.

    
    # gollum


You can access to your wiki page through _[http://localhost:4567](http://localhost:4567)_.


# Problems & Solutions




## Encoding issue


In my system, I couldn't create a new page and edit some pages. When I tried to create one, it shows the following error message.


<blockquote>'''
Encoding::CompatibilityError at /create
incompatible character encodings: UTF-8 and ASCII-8BIT
'''</blockquote>


[caption id="attachment_290" align="aligncenter" width="1212"][![create_error](http://yulistic.com/wp-content/uploads/2015/09/Selection_001.jpg)](http://yulistic.com/wp-content/uploads/2015/09/Selection_001.jpg) Cannot create a new page[/caption]

I was not familiar with ruby system, so I decided to workaround this issue. To workaround it, I used _**rugged **_**adapter** instead of _grit_ which is default. ([Git adapters in gollum](https://github.com/gollum/gollum/wiki/Git-adapters))


### Install rugged_adapter


For the installation of _rugged_adapter_ refer to [_rugged_adapter_ github site](https://github.com/gollum/rugged_adapter).

Briefly, you can install _rugged_ adapter with following command.

    
    # gem install --pre gollum-rugged_adapter


Then, _rugged_ adapter can be adopted by _gollum_ with the following options.

    
    # gollum --adapter rugged


But, it does not run because of the following mime-type error.


### Mime-types issue in rugged adapter


After installing _rugged_ adapter, _gollum_ does not run because of the mime-types version mismatch problem. This issue has already been filed ([link](https://github.com/gollum/rugged_adapter/issues/9)).

    
    # gollum --adapter rugged
    /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/specification.rb:2112:in `raise_if_conflicts': Unable to activate gollum-rugged_adapter-0.4, because mime-types-1.25.1 conflicts with mime-types (~> 2.6) (Gem::ConflictError)
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/specification.rb:1280:in `activate'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems.rb:198:in `rescue in try_activate'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems.rb:195:in `try_activate'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:126:in `rescue in require'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:39:in `require'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/gems/gollum-lib-4.1.0/lib/gollum-lib.rb:10:in `<top (required)>'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/gems/gollum-4.0.0/lib/gollum/app.rb:4:in `<top (required)>'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
            from /home/yulistic/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/gems/gollum-4.0.0/bin/gollum:192:in `<top (required)>'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/bin/gollum:23:in `load'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/bin/gollum:23:in `<main>'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/bin/ruby_executable_hooks:15:in `eval'
            from /home/yulistic/.rvm/gems/ruby-2.2.1/bin/ruby_executable_hooks:15:in `<main>'


As the issue has not been solved yet, I modified the gemspec file of _grit_. (Just release constraints of _grit_ dependency, as I'm not going to use _grit_.)

Open the _grit_'s gemspec file and modify it. In my case, I installed _ruby_ without root permission, so it was in my home directory.

    
    # vim ~/.rvm/gems/ruby-2.2.1/specifications/gitlab-grit-2.7.3.gemspec


Modify the file like below.

    
     27     if Gem::Version.new(Gem::VERSION) >= Gem::Version.new('1.2.0') then
     28       s.add_runtime_dependency(%q<charlock_holmes>, ["~> 0.6"])
     29       s.add_runtime_dependency(%q<posix-spawn>, ["~> 0.3"])
     30       # Modified by yulistic.
     31       # s.add_runtime_dependency(%q<mime-types>, ["~> 1.15"])
     32       s.add_runtime_dependency(%q<mime-types>, ["~> 2.6"])
     33       s.add_runtime_dependency(%q<diff-lcs>, ["~> 1.1"])
     34       s.add_development_dependency(%q<mocha>, [">= 0"])
     35     else
    


After modifying it, you can run _gollum_ and update pages normally.

    
    # gollum --adapter rugged




## Other issues




### git configuration (user.name & user.email)




When you try to update pages, it may requires git _user.name_ and_ user.email_ to be configured.




[caption id="attachment_299" align="aligncenter" width="1207"][![git config error (user.name)](http://yulistic.com/wp-content/uploads/2015/09/Selection_002.jpg)](http://yulistic.com/wp-content/uploads/2015/09/Selection_002.jpg) git config error (user.name)[/caption]


In the case, just set the configuration as below.




    
    # git config user.name "yulistic"


You can check your current configuration.

    
    # git config user.name
    yulistic


As the same way, _user.email_ can be configured.


### Add public key to Bitbucket


You don't need to type in password every time pushing. Refer to [link](https://confluence.atlassian.com/bitbucket/add-an-ssh-key-to-an-account-302811853.html).

For key generation, refer to the post: [[Linux] Login SSH without password input](http://yulistic.com/linux-2/284).


---





#  Remarks





	
  * How to pull/push automatically when update locally?


