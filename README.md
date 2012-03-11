Module 1 - Installing the Stack
===============================

Getting Started on OSX
----------------------
1. Install basic build tools from https://github.com/kennethreitz/osx-gcc-installer/downloads.  Xcode broke GCC support recently, so you won't be able to compile Rubygems properly with XCode's version of GCC.  Install Kenneth's tools.
2. Install rvm from http://beginrescueend.com/
  2.1.  Don't forget to either `source ~/.bash_profile` or restart your Terminal.
3. Install ruby 1.9.2 using `rvm install 1.9.2`
4. Setup 1.9.2 as the default using `rvm use 1.9.2 --default`
5. Install Homebrew from http://mxcl.github.com/homebrew/
6. Install git using `brew install git`
7. Configure git.
8. Register for a github.com account if you don't have one @ http://github.com
9. Checkout our project using `git clone https://github.com/jordantcox/com.nerdery.Blogotron`.
10. cd to your project's directory using `cd com.nerdery.Blogotron`
11. Create a branch to work in using `git branch johns_training`
12. Switch to that branch using `git checkout johns_training`
13. Run `bundle install` to setup all the gems
14. Tada!  Run `rails server` and get to coding!

### Troubleshooting OSX
If `rvm install 1.9.2` results in the error message "The provided compiler '/usr/bin/gcc' is LLVM based, it is not yet fully supported by ruby and gems, please read `rvm requirements`.", first ensure that you followed step 1 above. If the error still occurs, type the following at a command prompt:

	export CC=/usr/bin/gcc-4.2
	rvm install 1.9.2

This will force rvm to use the correct version of GCC, and should allow you to install Ruby successfully. 

Getting Started on Linux
------------------------
1. Install build-essentials (usually `sudo apt-get install build-essentials`)
2. Install rvm from http://beginrescueend.com/
  2.1.  Don't forget to either `source ~/.bash_profile` or restart your Terminal.
3. Install ruby 1.9.2 using `rvm install 1.9.2`
4. Setup 1.9.2 as the default using `rvm use 1.9.2 --default`
5. Install git using `sudo apt-get install git`
6. Configure git.
7. Register for a github.com account if you don't have one @ http://github.com
8. Checkout our project using `git clone https://github.com/jordantcox/com.nerdery.Blogotron`.
9. cd to your project's directory using `cd com.nerdery.Blogotron`
10. Create a branch to work in using `git branch johns_training`
11. Switch to that branch using `git checkout johns_training`
12. Run `bundle install` to setup all the gems
13. Tada!  Run `rails server` and get to coding!

Getting Started on Windows
--------------------------
1. Install the Rails installer from http://railsinstaller.org/
2. Install git using from http://code.google.com/p/msysgit/
3. Configure git.
4. Register for a github.com account if you don't have one @ http://github.com
5. Checkout our project using `git clone https://github.com/jordantcox/com.nerdery.Blogotron`.
6. cd to your project's directory using `cd com.nerdery.Blogotron`
7. Create a branch to work in using `git branch johns_training`
8. Switch to that branch using `git checkout johns_training`
9. Run `bundle install` to setup all the gems
10. Tada!  Run `rails server` and get to coding!

Module 2 - Building Your First Object
=====================================
1. Copy config/database.yml.skel to config/database.yml
2. rails generate resource Article
3. Edit db/migrate/CreateArticle to include:

		class CreateArticles < ActiveRecord::Migration
			def change
				create_table :articles do |t|
					t.string :content
					t.string :title

					t.timestamps
				end
			end
		end

4. Update app/controllers/articles_controller.rb to have an index action that will grab all articles from the database:

	class ArticlesController < ApplicationController
		def index
			@articles = Article.all
		end
	end

5. Create a basic app/views/articles/index.html.erb to render out our articles:

	<% @articles.each do |article| %>
		<h1><%= article.title %></h1>
		<p><%= article.content %></p>
	<% end %>