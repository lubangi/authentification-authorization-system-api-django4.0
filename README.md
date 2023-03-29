# Full-stack-Django-and-React
This is the part 1 of my project Social Media App using Django Posgresql and react

step:

setup django and start a project
...............
step 1 creating a folder djangoproject/djangoreact
setp 2 creating a virtual env python3 -m venv venv and activate it with: source venv/bin/activate
step 3 creating the requirements.txt file and add the version of django to install
    Django==4.0
step 4 on terminal install the requirements with: pip install -r requirements.txt 
step 5 on terminal verify the django version with: python3 -m django --version
step 6 on terminal start the django project with :  django-admin startproject Coreroot .
step 7 on terminal ls to see the folder structure , 3 files project manage.py and venv
step 8 on the terminal launch the migrate script to initialize the database with:  python3 manage.py migrate
step 8 verify the migration with ls , you should see the database db.sqlite3
    “Migrations are just a way to propagate changes made to the model in the database schema. As Django also comes with some models (such as the User model you can use for authentication), we need to apply these migrations. When we write our own models, we’ll also be creating migrations files and migrating them”
step 9 on terminal ,run the server with : python3 manage.py runserver and open the link shown in the termial to view the server page : http://127.0.0.1:8000/
    to quit the server run : ctrl+c

step 10 “we installed Django and started a Django”
......................



folder structure
..............................
“manage.py: This is a utility provided by Django for many different needs. It’ll help you create projects and applications, run migrations, start a server, and so on.”

“CoreRoot: This is the name of the project we’ve created with the django-admin command. It contains files such as the following:”

        “urls.py: This contains all the URLs that will be used to access resources in the project”
        “wsgi.py: This file is basically used for deployment but also as the default development environment in Django.”
        “asgi.py: Django also supports running asynchronous codes as an ASGI application”
        “settings.py: This contains all the configurations for your Django projects. You can find SECRET_KEY, the INSTALLED_APPS list, ALLOWED_HOST, and so on.”
..................................


configure database
........................................................
on main terminal : download prosgresql from brew with : brew install postgresql@14
con main terminal : heck version with :psql --version
on the vscode terminal : add postgresql adapter for python wich is psycopg in the requirements.txt with psycopg2_binary==2.9.2
on the vs terminal install postgresql adapter for python wich is psyconfig with : pip3 install psycopg2_binary
on the vs terminal to check version of psycopg2-binary , run : pip3 show psycopg2-binary
on the main terminal connect to posgresql with the user  , on the terminal , run: psql postgres
    for more info : https://www.sqlshack.com/setting-up-a-postgresql-database-on-mac/
    result :
    lionnel@LIONNELs-MacBook-Pro ~ % psql postgres
    psql (14.7 (Homebrew))
    Type "help" for help.

on the main terminal ,creating a new database :
    CREATE DATABASE coredb;

on the main terminal ,creating a user for the db:
    CREATE USER core WITH PASSWORD 'wCh29&HE&T83'; // user = core , pwd = wCh29&HE&T83

on the main terminal,  give root privileges to the user:
    GRANT ALL PRIVILEGES ON DATABASE coredb TO core

on the main terminal, allow user to create db on the posgresal server:

    ALTER USER core CREATEDB;

...................................................



connecting the database to the django project
...................................................

this require some configurqtions, open the seetings.py in the project
under DATABASE:
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
    the django project is using sqlite3 by defqult, we have to chqnge it so that it cans use posgresql
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.postgresql_psycopg2',
                'NAME': coredb,
                'USER': 'core',
                   'PASSWORD': 'wCh29&HE&T83',
                'HOST': 'localhost',
                'PORT': '5432',
            }
        }
After the change of the db engine:
    run the server  : python3 manage.py runserver 
    migrate the database with : python3 manage.py migrate

Note: the posgresql server must be running on port 5432, 127.0.0.1, tcp/ip port
      the django server should be running on port 8000, http port, 127.0.0.1/8000
Tip: on mac the main termianl for psql, in vscode two terminal, on for django server  running and other congiguration and update
Tip : learn how to view which port is used

now with the stever up and running, we have to test with an HTTP request client (like postman, insomnia)
    lik insomnia : https://insomnia.rest/download

................................................................


chap 2 Organizing a project
...........................................

project
applications

create new app in the project:
..............................

-on the third terminal , run : “django-admin startapp core” //core is the name of the app
- remove all the files in the app folder except :“apps.py file and the __init__.py”
...............................



creating the first model User
    the user model will wb created inside the app folder(core), before creatig the model we nned create an aspplication called user inside the app folder(core)
........
on the third terminal:
cd core
django-admin startapp user // this will create an new app inside the global app core

the create the user model in core/user/models.py 
then create the usermanager model core/user/models.py
then adding the label for the application in the apps.py from the app user
    label  = 'core_user'
then register the user app in the settingd.py from project CoreRoot
    'core.user'
telling django to use this user mdel for the  autehentification  model
    in the settings.py from the project CreateRoote
        AUTH_USER_MODEL = 'core_user.User'
then migrate the db
    from the third terminal run:
        python3 manage.py makemigratons

data_user = {
    "email": "testuser@yopmail.com",
    "username": "john-doe",
    "password": "12345",
    "first_name": "John",
    "last_name": "Doe"
}
user =User.objects.create_user(**data_user)






