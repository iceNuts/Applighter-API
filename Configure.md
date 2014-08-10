Configure Server 
===================

This works for Ubuntu Debug server, auto-script is needed to deploy production server.

- Install Git

```
$ sudo apt-get install git
```

- Get The Newest Code

```
$ sudo git clone https://github.com/liuyuxiao/applighter.git
$ sudo git pull origin dev
$ git checkout dev
```

- Install Project Dependencies

```
$ sudo easy_install pip
$ sudo apt-get install redis-server
$ sudo pip install -r requirements.txt
$ sudo cd OSS_PYTHON_SDK
$ sudo python setup.py install
```

- Install [MongoDB](http://www.mongodb.org/downloads)

- Remember to Check Everything Works

```
$ sudo mongo
$ sudo redis-server
$ sudo rqworker -c worker_setting
$ sudo python manage.py syncdb
$ sudo python manage.py runserver 0.0.0.0:80
```

Then you need the test data loaded, simply find TEST.md in the same repo.

Remeber to use cmd [screen](http://thingsilearned.com/2009/05/26/gnu-screen-super-basic-tutorial/) to make terminal powerful.
































