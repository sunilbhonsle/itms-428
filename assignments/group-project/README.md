# OVERVIEW

This folder contains all the materials needed to setup a database for the ITMS 428 group project.

See Google Drive folder [here](https://drive.google.com/open?id=1QxmZx0Z8Zj2jHo1opDDUPcvPuexvju1t).

# EXTRA SETUP FOR LINUX

If you're using Linux, (I tested this on Ubuntu), you'll need to run the following command BEFORE setting up Python.

`apt-get install libmysqlclient-dev python-dev libssl-dev`

This is because the 'mysqlclient' package is built from source with the version I'm using, at least for Linux.

It presumably needs `libmysqlclient-dev`'s source files, as well as `python-dev`'s source files too.

# CLONE THIS REPO

Install `git` and run `git clone https://github.com/HenryFBP/itms-428.git`, or download this project as a .ZIP file.

# SETUP DATABASE

I'll have you all use MySQL because of its popularity, and because it's easy to install on Windows, Linux, and OSX.

1. Download & install WAMP/LAMP/XAMPP/MAMP
    - [I use Windows!](http://www.wampserver.com/en/)
    - [I use Linux!](https://www.linode.com/docs/web-servers/lamp/install-lamp-stack-on-ubuntu-16-04/)
    - [I, for some inconcievable reason, use Solaris!](https://www.apachefriends.org/index.html)
    - [I use OSX!](https://www.mamp.info/en/)

      (P.S. If MAMP for OSX sucks, use XAMPP. It's cross-platform.)

 2. Find out the default username and password.

    It _might_ be different for different OSes. Not sure.

    You will need this for the Python step.

# SETUP PYTHON

1. Install [Python 3.6.*](https://www.python.org/downloads/).

2. Make sure `pip` is installed. To test this, run `pip` anywhere.

3. Inside this folder in this repository, run `pip install pipenv`.
   This installs a module for Python called 'pipenv', which I use to manage dependencies.
   You may notice a file called `Pipfile`. That's where I put all the dependencies!
   
4. Inside this folder in this repository, run `pipenv install`.
   
   This tells pipenv to create a virtual environment, segregated from your system's Python
   installation, that has the dependencies located in the Pipfile.

5. Make a file in this folder in this repository called `login_info.txt`.

   On the first line, put the username to login to MySQL.
   On the second line, put the password to login to MySQL.
   
   This file will NOT be tracked by Git, due to the `/.gitignore` file at the repo's root.
   
   The reason I have you do this is so that if one were to fork this repo, my personal login
   info would not be forced upon you, and your copy would not contain this.
   
That's it for setup!

To run any script, use

    pipenv run python script_name.py


To run my database setup script, run

    pipenv run python setup.py

# RUNNING MY FLASK EXAMPLES

Inside this folder, there is a `flask` folder.

Move into that folder.

To run my Flask web apps contained inside that folder, simply run:

	pipenv run python cool_app.py
  
# NOTES

## DEPENDENCY HELL
Should I ever add any dependencies to this project's `Pipfile`, and you find yourself
getting errors like:

    ModuleNotFoundError: No module named 'flaskext'

Run `pipenv install` to update your Python virtual environment.

## HOW DO I LOGIN?

MySQL user creds can be found inside of `users.py`.

User logins can be found in `data/mysql_sample_db`, under the
`UsersDatabase` class.

## FOR LINUX USERS

### Can't login to MySQL server with correct credentials

This section is courtesy of Dennis, who uses Lubuntu.

If you use Linux, speficially *buntu distros, you may have trouble
logging into the MySQL server, even with correct creds.

His problem ended up being a MySQL plugin called `auth_socket` that
essentially made his life hell for a couple weeks.

See [this link](https://stackoverflow.com/a/43659857/4262535) for the
Stack Overflow comment that fixed his problem.

If it doesn't fix the issue, there are a plethora of other guides
available online. A fresh install of EVERYTHING MYSQL, like using
`sudo apt-get purge --remove <PACKAGE_NAME>`, might work.