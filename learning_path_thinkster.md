Thinkster Django Angular tutorial
================================================================================

## Chapter 00

### Learning Django and AngularJS

In this tutorial you will build a simplified Google+ clone called “Not Google Plus” with Django and AngularJS.

Before we hit the proverbial books and learn to build a rich, modern web application with Django and Angular, let's take a moment to explore the motivations behind this tutorial and how you can get the most out of it.

**What is the goal of this tutorial?**

Here at Thinkster, we strive to create high value, in depth content while maintaining a low barrier to entry. We release this content for free with the hope that you find it both exciting as well as informative.

Each tutorial we release has a specific goal. In this tutorial, that goal is to give you a brief overview of how Django and AngularJS play together and how these technologies can be combined to build amazing web applications. Furthermore, we place a heavy emphasis on building good engineering habits. This includes everything from considering the tradeoffs that come from making architectural decisions, to maintaining high quality code throughout your project. While these things may not sound like fun, they are key to becoming a well-rounded software developer.

**Who is this tutorial for?**

Every author must answer this difficult question. Our goal is to make this tutorial useful  for novices as well as experienced developers.

For those of your who are in the early days of your software development careers, we have tried to be thorough and logical in our explanations as possible, while still making the text flow fluidly; we try to avoid making intuitive leaps where doing so makes sense.

For those of you who have been around the block a few times, and perhaps are just interested in learning more about Django or AngularJS, we know you don't need the basics explained to you. One of our goals when writing this tutorial was to make it easy to skim. This allows you to use your existing knowledge to speed up the reading process and identify where unfamiliar concepts are presented so you can grok them quickly and move on.

We want to make this tutorial accessible to anyone with enough interest to take the time necessary to learn and understand the concepts presented.

**A brief interlude about formatting**

Throughout this tutorial, we strive to maintain consistent formatting. This section details what that formatting looks like and what it means.

* When presenting a new code snippet, we will present the snippet in it's entirety and then walk through it line-by-line as necessary to cover new concepts.
* Variable names and file names appear in-line with special formatting: `thinkster_django_angular/settings.py`.
* Longer code snippets will appear on their own lines:

        def is_this_google_plus():
            return False

* Terminal commands also appear on their own line, prefixed by a `$`:

        $ python manage.py runserver

* Unless otherwise specified, you should assume that all terminal commands are run from the root directory of your project.
 
**A word on code style**

Where possible, we opt to follow style guides created by the Django and Angular communities.

For Django, we follow [PEP8](http://legacy.python.org/dev/peps/pep-0008/) strictly and try our best to adhere to [Django Coding style](https://docs.djangoproject.com/en/1.7/internals/contributing/writing-code/coding-style/).

For AngularJS, we have adopted John Papa's [AngularJS Style Guide](https://github.com/johnpapa/angularjs-styleguide). We also adhere to [Google's JavaScript Style Guide](https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml) where it makes sense to do so.

**A humble request for feedback**

At the risk of sounding cliche, we would not have a reason to make this tutorial if not for you. Because we believe that your success is our success, we invite you to contact us with any thoughts you have about the tutorial. You can reach us via the Olark box in the bottom-right corner of the screen, via Twitter at [@jamesbrwr](http://twitter.com/jamesbrwr) or [@GoThinkster](http://twitter.com/gothinkster), or by emailing [support@thinkster.io](mailto:support@thinkster.io).

We welcome criticism openly and accept praise if you believe it is warranted. We're interested in knowing what you like, what you don't like, what you want to know more about, and anything else you feel is relevant.

If you are too busy to reach out to us, that's OK. We know that learning takes a lot of work. If, on the other hand, you want to help us build something amazing, we await your mail.

**A final word before we begin**

It is our experience that the developers who gain the most from our tutorials are the ones who take an active approach to their learning.

We `strongly` recommend you type out the code for yourself. When you copy and paste code, you don’t interact with it and that interaction is in turn what makes you a better developer.

In addition to typing the code yourself, do not be afraid to get your hands dirty; jump in and play around, break things and build missing features. If you encounter a bug, explore and figure out what is causing it. These are the obstacles we as engineers must tackle multiple times a day, and have thus learned to embrace these explorations as the best source of learning.

Let's build some software.

**Setting up your environment**

The application we will be building requires a non-trivial amount of boilerplate. Instead of spending time setting up your environment, which is not the purpose of this tutorial, we have created a boilerplate project to get you started.

You can find the boilerplate project on Github at [brwr/thinkster-django-angular-boilerplate](https://github.com/brwr/thinkster-django-angular-boilerplate). The repository includes a list of commands you need to run to get everything running.


    If you are interested in a detailed appendix on setting up your environemnt, reach out to [@jamesbrewer](http://twitter.com/jamesbrwr) on Twitter.


Go ahead and follow the setup instructions now.


**Follow the instructions to set up your environment**

**Checkpoint**

If all went well running the server with `python manage.py runserver` should allow you to visit `http://localhost:8000/` in your browser. The page will be blank except for the navigation bar at the top. The links in the navigation bar currently do nothing.


**Make sure your environment is running by visiting `http://localhost:8000/`**

## Chapter 01

### Extending Django's built-in User model

Django has a built-in `User` model that offers a lot of functionality. The problem with `User` is that the model cannot be extended to include more information. For example, we will be giving our users a tagline to display on their profile. `User` does not have a tagline attribute and we cannot add one ourselves.

`User` inherits from `AbstractBaseUser`. That is where `User` gets most of it's functionality. By creating a new model called `Account` and inheriting from `AbstractBaseUser`, we will get the necessary functionality of `User` (password hashing, session management, etc) and be able to extend `Account` to include extra information, such as a tagline.

In Django, the concept of an "app" is used to organize code in a meaningful way. An app is a module that houses code for models, view, serializers, etc that are all related in some way. By way of example, our first step in building our Django and AngularJS web application will be to create an app called `authentication`. The `authentication` app will contain the code relevent to the `Account` model we just talked about as well as views for logging in, logging out and register.

Make a new app called `authentication` by running the following command:

    $ python manage.py startapp authentication


    Make a Django app named `authentication`


**Creating the Account model**

To get started, we will create the `Account` model we just talked about.

Open `authentication/models.py` in your favorite text editor and edit it to reflect the following:

    from django.contrib.auth.models import AbstractBaseUser
    from django.db import models

    class Account(AbstractBaseUser):
        email = models.EmailField(unique=True)
        username = models.CharField(max_length=40, unique=True)

        first_name = models.CharField(max_length=40, blank=True)
        last_name = models.CharField(max_length=40, blank=True)
        tagline = models.CharField(max_length=140, blank=True)

        is_admin = models.BooleanField(default=False)

        created_at = models.DateTimeField(auto_now_add=True)
        updated_at = models.DateTimeField(auto_now=True)

        objects = AccountManager()

        USERNAME_FIELD = 'email'
        REQUIRED_FIELDS = ['username']

        def __unicode__(self):
            return self.email

        def get_full_name(self):
            return ' '.join([self.first_name, self.last_name])

        def get_short_name(self):
            return self.first_name


    Make a new model in `authentication/models.py` called `Account`

Let's take a closer look at each attribute and method in turn.

    email = models.EmailField(unique=True)

    # ...

    USERNAME_FIELD = 'email'

Django's built-in `User` requires a username. That username is used for logging the user in. By contrast, our application will use the user's email address for this purpose.

To tell Django that we want to treat the email field as the username for this model, we set the `USERNAME_FIELD` attribute to `email`. The field specified by `USERNAME_FIELD` must be unique, so we pass the `unique=True` argument in the email field.

    username = models.CharField(max_length=40, unique=True)

Even though we will log in with our email address, we still want the user to have a username. We need some to display on their posts and profile page. We will also use the username in our URLs, so the username must be unique. To this end, we pass the `unique=True` argument in the username field.

    first_name = models.CharField(max_length=40, blank=True)
    last_name = models.CharField(max_length=40, blank=True)
 
Ideally we should have a more personal way to reference our users. Because we understand that not all users are comfortable giving out their personal details, we make the `first_name` and `last_name` fields optional by passing the `blank=True` argument.

    tagline = models.CharField(max_length=140, blank=True)

As mentioned before, the `tagline` attribute will be displayed on the user's profile. This gives the profile a hint of the user's personally, so it is worth including.

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

The `created_at` field records the time that the `Account` object was created. By passing `auto_now_add=True` to `models.DateTimeField`, we are telling Django that this field should be automatically set when the object is created and non-editable after that.

Similar to `created_at`, `updated_at` is automatically set by Django. The difference between `auto_now_add=True` and `auto_now=True` is that `auto_now=True` causes the field to update each time the object is saved.

    objects = AccountManager()

When you want to get a model instance in Django, you use an expression of the form `Model.objects.get(**kwargs)`. The `objects` attribute here is a `Manager` class whose name typically follows the `<model name>Manager` convention. In our case, we will create an `AccountManager` class. We will do this momentarily.

    REQUIRED_FIELDS = ['username']

We will be displaying the username in multiple places. To this end, having a username is not optional, so we include it in the `REQUIRED_FIELDS` list. Normally the `required=True` argument would accomplish this goal, but because this model is replacing the `User` model, Django requires us to specify required fields in this way.

    def __unicode__(self):
        return self.email

When working in the shell, as we will see shortly, the default string representation of an `Account` object looks something like `<Account: Account>`. Because we will have many different accounts, this is not very helpful. Overwriting `__unicode__()` will change this default behavior. Here we choose to show the user's email instead. The string representation of an account with the email `james@notgoogleplus.com` will now look like `<Account: james@notgoogleplus.com>`.

    def get_full_name(self):
        return ' '.join([self.first_name, self.last_name])

    def get_short_name(self):
        return self.first_name

`get_full_name()` and `get_short_name()` are Django conventions. We won't be using either of these methods, but it is still a good idea to include them to comply with Django conventions.

**Making a Manager class for Account**

When substituting a customer user model, it is required that you also define a related `Manager` class the overrides the `create_user()` and `create_superuser()` methods.

With `authentication/models.py` still open, add the following class above the `Account` class:

    from django.contrib.auth.models import BaseUserManager


    class AccountManager(BaseUserManager):
        def create_user(self, email, password=None, **kwargs):
            if not email:
                raise ValueError('Users must have a valid email address.')

            if not kwargs.get('username'):
                raise ValueError('Users must have a valid username.')

            account = self.model(
                email=self.normalize_email(email), username=kwargs.get('username')
            )

            account.set_password(password)
            account.save()

            return account

        def create_superuser(self, email, password, **kwargs):
            account = self.create_user(email, password, **kwargs)

            account.is_admin = True
            account.save()

            return account

Like we did with `Account`, let's step through this file line-by-line. We will only cover new information.

    if not email:
        raise ValueError('Users must have a valid email address.')

    if not kwargs.get('username'):
        raise ValueError('Users must have a valid username.')

Because users are required to have both an email and a username, we should raise an error if either of these attributes are missing.

    account = self.model(
        email=self.normalize_email(email), username=kwargs.get('username')
    )

Since we haven't defined a `model` attribute on the `AccountManager` class, `self.model` refers to the `model` attribute of `BaseUserManager`. This defaults to `settings.AUTH_USER_MODEL`, which we will change in just a moment to point to the `Account` class.

    account = self.create_account(email, password, **kwargs)

    account.is_admin = True
    account.save()

Writing the same thing more than once sucks. Instead of copying all of the code from `create_account` and pasting it in `create_superuser`, we simply let `create_user` handle the actual creation. This frees up `create_superuser` to only worry about turning an `Account` into a superuser.

**Changing the Django AUTH_USER_MODEL setting**

Even though we have created this `Account` model, the command `python manage.py createsuperuser` (which we will talk more about shortly) still creates `User` objects. This is because, at this point, Django still believes that `User` is the model we want to use for authentication.

To set things straight and start using `Account` as our authentication model, we have to update `settings.AUTH_USER_MODEL`.

Open `thinkster_django_angular_tutorial/settings.py` and add the following to the end of the file:

    AUTH_USER_MODEL = 'authentication.Account'


    Change `settings.AUTH_USER_MODEL` to use `Account` instead of `User`

This line tells Django to look in the `authentication` app and find a model named `Account`. 

**Installing your first app**

In Django, you must explicitly declare which apps are being used. Since we haven't added our `authentication` app to the list of installed apps yet, we will do that now.

Open `thinkster_django_angular_boilerplate/settings.py` and append `'authentication',` to `INSTALLED_APPS` like so:

    INSTALLED_APPS = (
        ...,
        'authentication',
    )


    Install the `authentication` app

**Migrating your first app**

When Django 1.7 was released, it  was like Christmas in September! Migrations had finally arrived!

Anyone with a background in Rails will find the concept of migrations familiar. In short, migrations handle the SQL needed to update the schema of our database so you don't have to. By way of example, consider the `Account` model we just created. These models need to be stored in the database, but our database doesn't have a table for `Account` objects yet. What do we do? We create our first migration! The migration will handle adding the tables to the database and offer us a way to rollback the changes if we make a mistake.

When you're ready, generate the migrations for the `authentication` app and apply them:

    $ python manage.py makemigrations
    Migrations for 'authentication':
        0001_initial.py:
            - Create model Account
    $ python manage.py migrate
    Operations to perform:
        Synchronize unmigrated apps: rest_framework
        Apply all migrations: admin, authentication, contenttypes, auth, sessions
    Synchronizing apps without migrations:
        Creating tables...
        Installing custom SQL...
        Installing indexes...
    Running migrations:
        Applying authentication.0001_initial... OK


    From now on, the output from migration commands will not be included for brevity.



    Generate the migrations for the `authentication` app and apply them

**Making yourself a superuser**

Let's talk more about the `python manage.py createsuperuser` command from a few minutes ago.

Different users have different levels of access in any given application. Some users are admins and can do anywhere, while some are just regular users whose actions should be limited. In Django, a super user is the highest level of access you can have. Because we want the ability to work will all facets of our application, we will create a super user. That is what `python manage.py createsuperuser` does.

After running the command, Django will prompt you for some information and create an `Account` with superuser access. Go ahead and give it a try.

    $ python manage.py createsuperuser


    Make a new super user `Account`

**Checkpoint**

To make sure everything is properly configured, let's take a quick break and open Django's shell:

    $ python manage.py shell

You should see a new prompt: `>>>`. Inside the shell, we can get the `Account` we just created like so:

    >>> from authentication.models import Account
    >>> a = Account.objects.latest('created_at')

If everything went well, you should be able to access the various attributes of your `Account` object:

    >>> a
    >>> a.email
    >>> a.username


    Access the `Account` object you just created

## Chapter 02

### Serializing the Account Model
The AngularJS application we are going to build will make AJAX requests to the server to get the data it intends to display. Before we can send that data back to the client, we need to format it in a way that the client can understand; in this case, we choose JSON. The process of transforming Django models to JSON is called serialization and that is what we will talk about now.

As the model we want to serialize is called `Account`, the serializer we will create is going to be called `AccountSerializer`.

**Django REST Framework**

As part of the boilerplate project you cloned earlier, we have included a project called Django REST Framework. Django REST Framework is a toolkit that provides a number of features common to most web applications, including serializers. We will make use of these features throughout the tutorial to save us both time and frustration. Our first look at Django REST Framework starts here.

**AccountSerializer**

Before we write our serializers, let's create a `serializers.py` file inside our `authentication` app:

    $ touch authentication/serializers.py


    Create a `serializers.py` file inside the `authentication` app

Open `authentication/serializers.py` and add the following code and imports:

    from django.contrib.auth import update_session_auth_hash

    from rest_framework import serializers

    from authentication.models import Account


    class AccountSerializer(serializers.ModelSerializer):
        password = serializers.CharField(write_only=True, required=False)
        confirm_password = serializers.CharField(write_only=True, required=False)

        class Meta:
            model = Account
            fields = ('id', 'email', 'username', 'created_at', 'updated_at',
                      'first_name', 'last_name', 'tagline', 'password',
                      'confirm_password',)
            read_only_fields = ('created_at', 'updated_at',)

	def create(self, validated_data):
		return Account.objects.create(**validated_data)

	def update(self, instance, validated_data):
		instance.username = validated_data.get('username', instance.username)
		instance.tagline = validated_data.get('tagline', instance.tagline)

		instance.save()

		password = validated_data.get('password', None)
		confirm_password = validated_data.get('confirm_password', None)

		if password and confirm_password and password == confirm_password:
		instance.set_password(password)
		instance.save()

		update_session_auth_hash(self.context.get('request'), instance)

		return instance


    Make a serializer called `AccountSerializer` in `authentication/serializers.py`


    From here on, we will declare imports that are used in each snippet. These may already be present in the file. If so, they do not need to be added a second time.


Let's take a closer look.

    password = serializers.CharField(write_only=True, required=False)
    confirm_password = serializers.CharField(write_only=True, required=False)

Instead of including `password` in the `fields` tuple, which we will talk about in a few minutes, we explicitly define the field at the top of the `AccountSerializer` class. The reason we do this is so we can pass the `required=False` argument. Each field in `fields` is required, but we don't want to update the user's password unless they provide a new one.

`confirm_pssword` is similar to `password` and is used only to make sure the user didn't make a typo on accident.

Also note the use of the `write_only=True` argument. The user's password, even in it's hashed and salted form, should not be visible to the client in the AJAX response.

    class Meta:

The `Meta` sub-class defines metadata the serializer requires to operate. We have defined a few common attributes of the `Meta` class here.

    model = Account

Because this serializers inherits from `serializers.ModelSerializer`, it should make sense that we must tell it which model to serialize. Specifying the model creates a guarantee that only attributes of that model or explicitly created fields can be serialized. We will cover serializing model attributes now and explicitly created fields shortly.

    fields = ('id', 'email', 'username', 'created_at', 'updated_at',
              'first_name', 'last_name', 'tagline', 'password',
              'confirm_password',)


The `fields` attribute of the `Meta` class is where we specify which attributes of the `Account` model should be serialized. We must be careful when specifying which fields to serialize because some fields, like `is_superuser`, should not be available to the client for security reasons.

    read_only_fields = ('created_at', 'updated_at',)

If you recall, when we created the `Account` model, we made the `created_at` and `updated_at` fields self-updating. Because of this feature, we add them to a list of fields that should be read-only.

    def create(self, validated_data):
        # ...

    def update(self, instance, validated_data):
        # ...

Earlier we mentioned that we sometimes want to turn JSON into a Python object. This is called deserialization and it is handled by the `.create()` and `.update()` methods. When creating a new object, such as an `Account`, `.create()` is used. When we later update that `Account`, `.update()` is used.

    instance.username = attrs.get('username', instance.username)
    instance.tagline = attrs.get('tagline', instance.tagline)

We will let the user update their username and tagline attributes for now. If these keys are present in the arrays dictionary, we will use the new value. Otherwise, the current value of the `instance` object is used. Here, `instance` is of type `Account`.

    password = validated_data.get('password', None)
    confirm_password = validated_data.get('confirm_password', None)

    if password and confirm_password and password == confirm_password:
        instance.set_password(password)
        instance.save()

Before updating the user's password, we need to confirm they have provided values for both the `password` and `password_confirmation` field. We then check to make sure these two fields have equivelant values.

After we verify that the password should be updated, we much use `Account.set_password()` to perform the update. `Account.set_password()` takes care of storing passwords in a secure way. It is important to note that we must explicitly save the model after updating the password.


    This is a naive implementation of how to validate a password. I would not recommend using this in a real-world system, but for our purposes this does nicely.

    update_session_auth_hash(self.context.get('request'), instance)

When a user's password is updated, their session authentication hash must be explicitly updated. If we don't do this here, the user will not be authenticated on their next request and will have to log in again.

**Checkpoint**
By now we should have no problem seeing the serialized JSON of an `Account` object. Open up the Django shell again by running `python manage.py shell` and try typing the following commands:

    >>> from authentication.models import Account
    >>> from authentication.serializers import AccountSerializer
    >>> account = Account.objects.latest('created_at')
    >>> serialized_account = AccountSerializer(account)
    >>> serialized_account.data.get('email')
    >>> serialized_account.data.get('username')


    Make sure your `AccountSerializer` serializer is working



