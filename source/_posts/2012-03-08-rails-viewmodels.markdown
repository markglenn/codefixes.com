---
layout: post
title: "Rails ViewModels"
date: 2012-03-08 07:34
comments: true
categories: 
---
If you're in the Ruby community or use GitHub at all, you will have heard about a recent security issue with
GitHub's site that could allow an attacker access to various fields within the GitHub database.  This sounds
strangely similar to a SQL injection attack, however Rails is good with using proper, parameterized SQL. 
The one thing they don't do by default is to sanitize user input, something that we should all know about.
.NET has had a simple solution to this problem, ViewModels.

<!-- more -->

I've been working with Ruby and Rails for over a year professionally, but there has always been one thing
about Rails that has bothered me from the beginning.  When working with user input, always assume that it
is coming from a hostile party.  

The rails has a saying that really has been taken much further than it really should have been taken.  DRY,
or Don't Repeat Yourself, is a common statement.  One thing a developer doesn't want to do is duplicate 
anything, even if it's one line of code.  The easiest thing you can do to minimize duplication is to pass
the database models directly between the view and database.  As asinine as this may seem it's the default,
and the recommended approach for developing rails applications.

``` ruby
def show
  respond_with( @model = Model.find(params[:id]) )
end

def update
  @model = Model.find(params[:id])

  # Update the model without checking user input
  if @model.update_attributes( params[ :model ] )
    flash[ :notice ] = 'The model was successfully updated.'
  end

  respond_with @model
end
```

There has been recent talks about this now that this issue has been pushed into the front line due to the 
GitHub compromise.  Discussions have surrounded a few key topics: where should the security checks occur,
who's responsibility is it whitelist the correct attributes, how can we keep this DRY?  I believe all these
questions really miss the real issue here.  We need to isolate the user input from the database.  The onus of
responsibility shouldn't be in the model because the model should only care about validating data and representing
what is in the data store.  The responsibility shouldn't be put on the controller because this is a data 
integrity issue.  What we need is a new class of objects that are a barrier between the view and model, the 
view model.

The view model is a specific view of the data tightly coupled with the views.  For example, on a page that 
allows the user to change their email address, you shouldn't have to load the entire user model, and you
should never allow the user to submit a generic key/value hash to update their model for such a simple
form.  Instead, you should create a new model, not tied to ActiveRecord, that hosts just
the required fields.

``` ruby
class UserUpdateEmailAddressViewModel
  attr_accessible :user_id, :password, :email

  def user
    @user ||= User.find_with_password(@user_id, hash_password(@password, salt))
  end

  def user=( user )
    @user_id = user.id
    @email = user.email
  end

  def update( params )
    @user_id = params[ :id ]
    @email = params[ :email ]
  end

  def save
    user.update_attributes( :email => @email )
  end
end
```

While the prior example could be DRYed up a bit using a simple base class, I wanted to show the simplicity required
to remove the data from being accessed by the view.
