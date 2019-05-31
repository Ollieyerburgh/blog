---
layout: post
title:  "Getting Started With Rails (mac)"
date:   2019-05-18 18:23:36 +0100
description: My most recent post
---

This guide is specifically for Mac OS X. You can see how to install Rails on [Windows][windows-10] or [Linux][Linux] through one of these links.

As Ruby on Rails is based on Ruby, we first need to install Ruby.

Mac OS usually comes with Ruby pre-installed, however the pre-installed versions are usually outdated. 

To check whether you have Ruby installed, open your terminal (Press <kbd>cmd</kbd>+<kbd>space</kbd> to open your spotlight search, type terminal and hit return) and run the following
```
ruby -v
```
Rails 5 requires at least [Ruby 2.2.2+][rails-5-ruby-version] , whilst Rails 6 (newest) requires atleast [Ruby 2.5.0+][rails-6-ruby-version]


### Installing Ruby

To install Ruby, we’re first going to install Homebrew, a package management system which makes installing software easier on a Mac. 

To install Homebrew, run
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
After installing Homebrew, it’s possible to install Ruby by running the following command
```
brew install ruby
```
This is only recommended if you just want to run a few scripts. If you’re going to be developing multiple Ruby applications however, you should first install a Ruby version management tool. 

The Ruby version management tool that we’re going to use is RVM. RVM requires a package manager, which is why we first installed Homebrew.

To install RVM, we must first install gpg, an encryption program which checks the security of the RVM download. 
```
brew install cpg
```
Once this has completed, we must install the security key for RVM.
```
command curl -sSL https://rvm.io/mpapis.asc | gpg --import –
```
Before installing RVM, you must make sure that your Mac username doesn’t contain any spaces. If it does, follow the tutorial [here][change-account-name] to change the account name.

To install RVM, run the following
```
\curl -sSL https://get.rvm.io | bash
```
If you want to remove RVM from your machine, you can run rvm implode which will remove RVM completely from your machine.

Once RVM is installed, you must close and re open your terminal to refresh it. 

Use RVM to install the latest version of Ruby. As of writing, the [current recommended version][recommended-ruby-version] is version 2.6.3.
```
rvm install 2.6.3
```
Now you must specify to use that version by default
```
rvm use 2.6.3 --default	
```
To check whether the your Ruby version has been updated, run
```
ruby -v
```
Once you have the latest version of Ruby installed, it’s suggested that you install Bundler. Bundler is a tool that makes it easy to manage gems within a Ruby project.
```
$ gem install bundler
```
### Installing Rails
With Ruby installed through RVM and bundler installed, it's now time to install Rails.
```
gem install rails
```
This will install the current stable version of Rails

If you want an older version of Rails, run
```
gem install rails –v 5.0.0
```
To check whether Rails is installed, run 
```
rails -v
```
Rails is now installed, and you’re ready to create your first Rails application.

We’re going to name the rails project blog, but you can name it whatever you like.
```
rails new blog
```
This will create an application called Blog in the blog directory. Now switch to the folder
```
cd blog
```
Now you’re in the directory in the terminal, open the directory in your favourite text editor. I use VS Code, which can be found [here][vscode].

In most modern text editors, you can open the file structure by running a command
```
code .
```
You’ll see that Rails has automatically generated a series of files and folders. Most of the development work that you do will take place in the app/ folder. 

Find a table below which details what each file/folder does. [(source)][rails-guide]

| File/Folder  | Purpose |
| ------------- | ------------- |
| app/  | Contains the controllers, models, views, helpers, mailers, channels, jobs and assets for your application. You'll focus on this folder for the remainder of this guide.  |
| bin/  | Contains the rails script that starts your app and can contain other scripts you use to setup, update, deploy or run your application. |
| config/  | Configure your application's routes, database, and more. This is covered in more detail in [Configuring Rails Applications][config-rails].  |
| congig.ru  | Rack configuration for Rack based servers used to start the application. For more information about Rack, see the [Rack website][rack-website].  |
| db/  | Contains your current database schema, as well as the database migrations.  |
| Gemfile Gemfile.lock  | These files allow you to specify what gem dependencies are needed for your Rails application. These files are used by the Bundler gem. For more information about Bundler, see the [Bundler website][Bundler].  |
| lib/  | Extended modules for your application. |
| log/  | Application log files. |
| package.json  | This file allows you to specify what npm dependencies are needed for your Rails application. This file is used by Yarn. For more information about Yarn, see the [Yarn website][yarn-website]. |
| public/  | The only folder seen by the world as-is. Contains static files and compiled assets.  |
| Rakefile  | This file locates and loads tasks that can be run from the command line. The task definitions are defined throughout the components of Rails. Rather than changing Rakefile, you should add your own tasks by adding files to the lib/tasks directory of your application.  |
| README.md  | This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on.  |
| test/  | Unit tests, fixtures, and other test apparatus. These are covered in [Testing Rails Applications][testing-rails].  |
| tmp/  | Temporary files (like cache and pid files).  |
| vendor/  | A place for all third-party code. In a typical Rails application this includes vendored gems.  |
| .gitignore  | This file tells git which files (or patterns) it should ignore. See [GitHub - Ignoring files][git-ignore] for more info about ignoring files.  |
| .ruby-version  | This file contains the default Ruby version.  |

### Running Rails

To start your Rails application, run 

```
rails server
```
or

```
rails s
```
This will start a server running on localhost port 3000. To stop your Rails application from running, press <kbd>ctrl</kbd>+<kbd>c</kbd>.


 To visit your Rails application, go to [http://localhost:3000][localhost].

Hopefully everything has worked correctly, and you should see a lovely image notifying that you're on Rails.

![image](/assets/images/rails_welcome.png)

That's it for this tutorial. In our next tutorial, we will find our how to create posts on our website.


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
[windows-10]: https://gorails.com/setup/windows/10
[linux]: https://gorails.com/setup/ubuntu/18.10
[rails-5-ruby-version]: https://weblog.rubyonrails.org/2015/12/18/Rails-5-0-beta1/
[rails-6-ruby-version]: https://weblog.rubyonrails.org/2019/1/18/Rails-6-0-Action-Mailbox-Action-Text-Multiple-DBs-Parallel-Testing/
[change-account-name]: https://support.apple.com/en-gb/HT201548
[recommended-ruby-version]: https://www.ruby-lang.org/en/downloads/
[vscode]: https://code.visualstudio.com/
[rails-guide]: https://guides.rubyonrails.org/getting_started.html
[config-rails]: https://guides.rubyonrails.org/configuring.html
[rack-website]: https://rack.github.io/
[Bundler]: https://bundler.io/
[yarn-website]: https://yarnpkg.com/lang/en/
[testing-rails]: https://guides.rubyonrails.org/testing.html
[git-ignore]: https://help.github.com/en/articles/ignoring-files
[localhost]: http://localhost:3000