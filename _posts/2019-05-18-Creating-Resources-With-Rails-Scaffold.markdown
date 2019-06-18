---
layout: post
title:  "Creating Resources with Rails scaffold"
date:   2019-05-18 18:23:36 +0100
description: My first post
---
In this article we're going to learn how to create resources using Rails scaffold. If you manually create files to manage a resource in Rails, it can be time consuming and it's easy to make a mistake. By using Rails scaffold, the process is almost instant, and the methods to Create, Read, Update and Delete the resource will also be created.

As the application that we created [last time]({{ site.baseurl }}{% post_url 2019-05-18-Getting-Started-With-Rails %}) was for a blog, were going to create a Post resource. We’re going to utilise rails scaffold here, which automatically generates the models, views and controllers for a single resource. In this case, the resource that we are referring to is Post. We want our Post resource to have two fields, a body field and a title field. We can specify that we want these fields in our migration by adding the field names to the end of the scaffold command in the format fieldname:type.

```
$ rails g scaffold Post title:string body:text
```
You will see that a variety of files have been created.

_Note: You will see that a few files will be created that end in .jbuilder. This is because of the jBuilder gem that allows you to make JSON APIs. You can run ```gem uninstall jbuilder``` to remove this gem. Further scaffolds won't create these files if you do this._
<br/><br/>
<div style="text-align: center"><img src="/assets/images/scaffold_files.png" style="max-width: 400px"></div>
<br/>
Now start the server:

```
$ rails s
```

Navigate to [http://localhost:3000][localhost], and you will see that that is an error.
<br/><br/>
![image](/assets/images/migration_error.png)
<br/><br/>
This ActiveRecord::PendingMigrationError indicates that we have made a migration to change the database, but the schema has not been updated.

To resolve this error first close the Rails process by pressing <kbd>ctrl</kbd><kbd>+</kbd><kbd>c</kbd> and then migrate the database.

``` 
$ rails db:migrate 
```
Start your rails application again and navigate to [http://localhost:3000/posts][localhost/posts].

You will see a page which contains all the Posts in the database. You can Create, Read, Update and Delete Posts now because Rails has generated the methods for you in app/controllers/posts_controller.rb.  

### Summary
We wanted to add a resource to our Rails application, but there’s many files to create in order to do this. By using Rails scaffold, we can easily generate files for a resource with CRUD functionality.







[localhost]: http://localhost:3000
[localhost/posts]: http://localhost:3000/posts