# Welcome to Tutorial!

Hi, this is a simple tutorial related to ARORA project. In this tutorial, you will learn about how to primarily use Django-REST-framework and Retrofit2.


# Django-REST-framework
## Setup
Let's start with Django-rest-framework. Before we get started, please make sure:
1. You have a python3 on your machine. Though Python is cross-platform, I recommend you use Linux or Linux VM as your operating system.
 
2. You have installed Django and Django-rest-framework on your python. If you haven't
	> pip(pipenv) install django
	> pip(pipenv) install djangorestframework

3. Have created a Django Project properly. If you use Pycharm as your IDE, Things should be easy. If you do not use Pycharm, you can use
	> django-admin startproject < YOUR_PROJECT_NAME > .    

4. Have started an application, example1.
	> python3 manage.py startapp example1


5. You have example1, example2 and rest_framework at **INSTALLED_APPS** list which is at  *< root_dir>/ djangorest_example/setting.py* . 

        INSTALLED_APPS = [  
        'django.contrib.admin',  
	    'django.contrib.auth',  
        'django.contrib.contenttypes',  
        'django.contrib.sessions',  
        'django.contrib.messages',  
        'django.contrib.staticfiles',  
      
        'example1', 
        'rest_framework',  
       ]

Here is a [tutorial](https://wsvincent.com/django-rest-framework-tutorial/) could be help at set-up.
## FIie structure and explanation
After we have done the set-up, the whole project should look like this.
![enter image description here](https://lh3.googleusercontent.com/CAbsN_SgS47Dvu1yrGXq6M68HYC0CsG8ET-WWknex3Qeukezihxp_NPHA59Mxm6B2GSCYJ0vRrY) 
And don't forget to create serializers.py and urls.py manually under every application.

Now, 
Let's take example1, one of our created application, as an example.

```mermaid
graph LR
A((example1)) -- - --> B(migrarions) 
B(migrarions) -- - --> C[__init__.py]
B(migrarions) -- - --> D{Other migration files}
A((example1)) -- - --> E(__init__.py) 
A((example1)) -- - --> F(admin.py *) 
A((example1)) -- - --> L(apps.py)
A((example1)) -- - --> G(models.py *)
A((example1)) -- - --> I(serializers.py *) 
A((example1)) -- - --> K(tests.py) 
A((example1)) -- - --> J(urls.py *)
A((example1)) -- - --> H(view.py *)
```
Note:
 1. The file structure of the application should like this figure. And please remeber those 		   files are vital for the application, and do not delete them casually, except migration files. And I will explain why migration files can be deleted at later content. 
 2. There are five files with STAR notation need us to work on. Let's get into there one by one. 

## Models.py
We can create our models at models.py. There can be more than one model in the models.py, which means there can be more than one model in an application.

Basically, Django database is based on ORM, this is to say, your database structure is determined by your code in model.py.

Let's bulid our model.
Click here to MODEL.PY

After we finish our code, then we do
> python3 manage.py makemigrations 

As you can see, there are two new files, 0001_initial.py and db.sqlite3. 
	![enter image description here](https://lh3.googleusercontent.com/lIksGDKRFNH-jMQKk02O0J87uAGkRs1XEBNReSGvu6fr2-7cU1WZE1D7coSVRUQvcc6evV9MEK8)

 - You can regard 0001_initial.py as the blueprint of the database.
 
 - db.sqlite3 is the brand new database created by the blueprint.
 - We use SQLite3 as our database by default. Of course, you can use
   other database you want, and your database setting is at *< root_dir>/ main_application/setting.py* .  
    
   
       DATABASES = {  
		   'default': {  
	   	        'ENGINE': 'django.db.backends.sqlite3',  
	   		    'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),   		
			}  
	    }


But we haven't done yet. Let's do
> python3 manage.py migrate
> 
![enter image description here](https://lh3.googleusercontent.com/srsTro62EmaJIp_5lbypVXpdrGXBVOY8atZSbOSR--7PpPekXmRQ7Vj9Pd1GYt8_18DC3NnG6Q4)

After you see a series of OK, our model part is done.

Note: If you have a drastic change on your model and you meet a weired and tough bug when you try modify your database by using **migrate**, I do recommand you delete all migration files and db.sqlite3 which is database. And try it again.  

## Serializers.py

Now we need a tool that can transform our data between model and JSON format.
Django REST Framework provides serializers to do this job. What we need to do is extend the built-in serializer to fit our requirement.

> Serializers allow complex data such as querysets and model instances
> to be converted to native Python datatypes that can then be easily
> rendered into  `JSON`,  `XML`  or other content types. Serializers
> also provide deserialization, allowing parsed data to be converted
> back into complex types, after first validating the incoming data.
> 
> The serializers in REST framework work very similarly to Django's 
> `Form`  and  `ModelForm`  classes. We provide a  `Serializer`class
> which gives you a powerful, generic way to control the output of your
> responses, as well as a  `ModelSerializer`  class which provides a
> useful shortcut for creating serializers that deal with model
> instances and querysets.
> 
> From Django REST Framework 

Let's start with our code.

Click here to SERIALIZERS.PY

## views.py 
Now, we are doing the core of an application. views.py determines how you RESTful server response the request.

There are different ways to write the code of this part, from low customized to highly customized. Here, I just provide a way which I think should be easy and clear.

Click here to VIEWS.PY


## urls.py 
Though we have done the core part of our application, but there is still no route to access our server. So, we have to set urls for our server.

REMEMBER: Do not forget add the urls of the application into the main application, which should be djangorest_example in this case.

< root_dir >/ djangorest_example/ urls.py 

    from django.contrib import admin  
    from django.urls import path, include  
      
    urlpatterns = [  
        path('admin/', admin.site.urls),  
      path('', include('example1.urls')),  
    ]


Click here to URLS.PY

## admin.py
We alomost done. But we want our admin site knows we have a new application. So, we need a register in admin.py.

Click here to ADMIN.PY

## Test

 1. Let's try create a new Model1 object by using [POSTMAN](https://www.getpostman.com/)
2. Oops, someting is wrong here, it shows m
![enter image description here](https://lh3.googleusercontent.com/L6j0qq2pbNddCVhezB7x2lAUAtw-x91rZVeNAxpVcF3yL61yC7f3QZ4kIupze3QNqI_GcGoD1uc)
 


## Summary 

 - Here are processing figure to show how it works.

GET 
```mermaid
graph LR
request -- . --> urls.py
urls.py -- route to the method --> views.py
views.py -- . --> models.py
models.py -- find the ojbect --> Database
Database -- result back --> serializers.py
serializers.py -- serialized data/JSON --> views.py
views.py --. --> response
```

POST/ PUT/ PATCH 
```mermaid
graph LR
request -- . --> urls.py
urls.py -- route to the method --> views.py
views.py -- . --> serializers.py
serializers.py -- deserialized data/Object --> models.py
models.py -- create/update the ojbect --> Database
Database -- result back success/failure --> views.py
views.py --. --> response
```

DELETE
```mermaid
graph LR
request -- . --> urls.py
urls.py -- route to the method --> views.py
views.py -- . --> models.py
models.py -- find the ojbect --> Database
Database -- result back success/failure --> views.py
views.py --. --> response
```

 - Build proper model is the first key step to create a good
   application.

   

## Switch to another file

All your files are listed in the file explorer. You can switch from one to another by clicking a file in the list.

## Rename a file

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Delete a file

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.


# Synchronization

Synchronization is one of the biggest features of StackEdit. It enables you to synchronize any file in your workspace with other files stored in your **Google Drive**, your **Dropbox** and your **GitHub** accounts. This allows you to keep writing on other devices, collaborate with people you share the file with, integrate easily into your workflow... The synchronization mechanism takes place every minute in the background, downloading, merging, and uploading file modifications.

There are two types of synchronization and they can complement each other:

- The workspace synchronization will sync all your files, folders and settings automatically. This will allow you to fetch your workspace on any other device.
	> To start syncing your workspace, just sign in with Google in the menu.

- The file synchronization will keep one file of the workspace synced with one or multiple files in **Google Drive**, **Dropbox** or **GitHub**.
	> Before starting to sync files, you must link an account in the **Synchronize** sub-menu.

## Open a file

You can open a file from **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Open from**. Once opened in the workspace, any modification in the file will be automatically synced.

## Save a file

You can save any file of the workspace to **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Save on**. Even if a file in the workspace is already synced, you can save it to another location. StackEdit can sync one file with multiple locations and accounts.

## Synchronize a file

Once your file is linked to a synchronized location, StackEdit will periodically synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be resolved.

If you just have modified your file and you want to force syncing, click the **Synchronize now** button in the navigation bar.

> **Note:** The **Synchronize now** button is disabled if you have no file to synchronize.

## Manage file synchronization

Since one file can be synced with multiple locations, you can list and manage synchronized locations by clicking **File synchronization** in the **Synchronize** sub-menu. This allows you to list and remove synchronized locations that are linked to your file.


# Publication

Publishing in StackEdit makes it simple for you to publish online your files. Once you're happy with a file, you can publish it to different hosting platforms like **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **WordPress** and **Zendesk**. With [Handlebars templates](http://handlebarsjs.com/), you have full control over what you export.

> Before starting to publish, you must link an account in the **Publish** sub-menu.

## Publish a File

You can publish your file by opening the **Publish** sub-menu and by clicking **Publish to**. For some locations, you can choose between the following formats:

- Markdown: publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).

## Update a publication

After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the **Publish now** button in the navigation bar.

> **Note:** The **Publish now** button is disabled if your file has not been published yet.

## Manage file publication

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.


# Markdown extensions

StackEdit extends the standard Markdown syntax by adding extra **Markdown extensions**, providing you with some nice features.

> **ProTip:** You can disable any **Markdown extension** in the **File properties** dialog.


## SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|


## KaTeX

You can render LaTeX mathematical expressions using [KaTeX](https://khan.github.io/KaTeX/):

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> You can find more information about **LaTeX** mathematical expressions [here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).


## UML diagrams

You can render UML diagrams using [Mermaid](https://mermaidjs.github.io/). For example, this will produce a sequence diagram:

```mermaid
sequenceDiagram
Alice ->> Bob: Hello Bob, how are you?
Bob-->>John: How about you John?
Bob--x Alice: I am good thanks!
Bob-x John: I am good thanks!
Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

Bob-->Alice: Checking with John...
Alice->John: Yes... John, how are you?
```

And this will produce a flow chart:

```mermaid
graph LR
A[Square Rect] -- Link text --> B((Circle))
A --> C(Round Rect)
B --> D{Rhombus}
C --> D
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEwNTQ4NzMxMSwtOTY3MzYzMzYsMjg0MD
Y1NzM2LC0zOTM5OTQ3MzAsODQ0ODEwMjAyLC00Njc0MjUyNjcs
MTg2NDY2MDY3NCwxOTIzNTgzNTY2LDEzMjUwNTYwODIsMTAyMD
A4NDM5MSwxNzEwMDIwMTk3LC0xNDcxMjY1OTI5LDIwMzczMzM0
NjUsLTE3MjU1NDc1NTksMTc1NzU2MTU1OF19
-->