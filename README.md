# travis-test
[![Build Status](https://travis-ci.org/elviswxy/travis-test.png)](https://travis-ci.org/elviswxy/travis-test)

首先，使[Travis CI](https://travis-ci.org/)通过`github OAuth`认证.

点击https://travis-ci.org/右上角的`Sign in with GitHub`按钮，输入自己的github账号和密码，并允许Travis CI的认证。

然后，激活`GitHub Service Hook`。

GitHub给用户提供了一个`Service Hook`接口,只要用户对host在github上的repository作用了一些action(比如push，pull)，就会触发相应的`Service Hook`。而Travis CI正是基于这个原理来trigger你的build。当你发起一个push操作时，就会trigger Travis CI的服务。

设置方法是访问Travis CI的profile，选择相应的repository打开Service Hook开关。

然后登陆你的github，访问具体的repository的Service Hook页面，确保设置了Travis CI Hook的github name和travis token。

#Installation travis in local computer

Make sure you have at least Ruby 1.9.3 (2.0.0 recommended) installed.

##Updating your Ruby

If you have an outdated Ruby version, you should use your package system or a Ruby Installer to install a recent Ruby.

Ubuntu:
```
$ sudo apt-get install python-software-properties
$ sudo apt-add-repository ppa:brightbox/ruby-ng
$ sudo apt-get update
$ sudo apt-get install ruby2.1 ruby-switch
$ sudo ruby-switch --set ruby2.1
```

Alternatively, you can use a Ruby version management tool such as rvm, rbenv or chruby. This is only recommended if you need to run multiple versions of Ruby.

You can of course always compile Ruby from source, though then you are left with the hassle of keeping it up to date and making sure that everything is set up properly.

##Troubleshooting

Ubuntu

On certain versions of Ubuntu (e.g., 13.10), you need to install the corresponding -dev package in order to build the C extension on which travis gem depends.

If you updated to Ruby 2.1 as shown above:
```
$ sudo apt-get install ruby2.1-dev
```
You can check your Ruby version by running ruby -v:
```
$ ruby -v
ruby 2.0.0p195 (2013-05-14 revision 40734) [x86_64-darwin12.3.0]
```
Then run:
```
$ gem install travis -v 1.7.7 --no-rdoc --no-ri
```
if you meet a bug: `Error: failed to build gem native extension`. Run
```
$ sudo apt-get install ruby2.1-dev
```
Now make sure everything is working:
```
$ travis version
1.7.7
```
##Development Version

You can also install the development version via RubyGems:
```
$ sudo gem install travis --pre
We automatically publish a new development version after every successful build.
```
#First test: helloworld

## Set the config of `.travis.yml`
给repository配置`.travis.yml`文件。该文件需要放置在repository的跟目录下。

`.travis.yml`文件是一个相当重要的文件，里面需要配置你所使用的语言、运行环境、构建工具、构建脚本、通知方式等。最重要的是设置语言，其它的都有相应的默认值。

这是我为了测试`hello world`设置的.travis.yml文件。主要测试目的是在结果文件中输出hello worl.


```
language: python

python:
    - '2.7'

script:
    - python helloworld.py

```
你可以使用一个`travis-lint`来检查你的yml文件是否是有效的。他是ruby写的一个gem，需要ruby的运行环境。安装方式在上面章节已经解释。你只需要在你的repository根目录下运行travis-lint即可进行检查。

想要更进一步的关于`.travis.yml`的配置请参见：http://about.travis-ci.org/docs/user/build-configuration/

完成配置后。现在发起一个push就可以trigger你在Travis CI的build。 这时候登陆Travis CI可以看到你的Build的状态和日志。

The results log of hello world python test, we can see the hello world is printed.
```
Using worker: worker-linux-docker-1cc16ef5.prod.travis-ci.org:travis-linux-7
system_info
Build system information
Build language: python
Build image provisioning date and time
Thu Feb  5 15:09:33 UTC 2015
Operating System Details
Distributor ID:	Ubuntu
Description:	Ubuntu 12.04.5 LTS
Release:	12.04
Codename:	precise
Linux Version
3.13.0-29-generic
Cookbooks Version
a68419e https://github.com/travis-ci/travis-cookbooks/tree/a68419e
GCC version
gcc (Ubuntu/Linaro 4.6.3-1ubuntu5) 4.6.3
Copyright (C) 2011 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
LLVM version
clang version 3.4 (tags/RELEASE_34/final)
Target: x86_64-unknown-linux-gnu
Thread model: posix
Pre-installed Ruby versions
ruby-1.9.3-p551
Pre-installed Node.js versions
v0.10.36
Pre-installed Go versions
1.4.1
Redis version
redis-server 2.8.19
riak version
2.0.2
MongoDB version
MongoDB 2.4.12
CouchDB version
couchdb 1.6.1
Neo4j version
1.9.4
RabbitMQ Version
3.4.3
ElasticSearch version
1.4.0
Installed Sphinx versions
2.0.10
2.1.9
2.2.6
Default Sphinx version
2.2.6
Installed Firefox version
firefox 31.0esr
PhantomJS version
1.9.8
ant -version
Apache Ant(TM) version 1.8.2 compiled on December 3 2011
mvn -version
Apache Maven 3.2.5 (12a6b3acb947671f09b81f49094c53f426d8cea1; 2014-12-14T17:29:23+00:00)
Maven home: /usr/local/maven
Java version: 1.7.0_76, vendor: Oracle Corporation
Java home: /usr/lib/jvm/java-7-oracle/jre
Default locale: en_US, platform encoding: ANSI_X3.4-1968
OS name: "linux", version: "3.13.0-29-generic", arch: "amd64", family: "unix"
git.checkout
0.08s$ git clone --depth=50 --branch=master git://github.com/elviswxy/travis-test.git elviswxy/travis-test
Cloning into 'elviswxy/travis-test'...
remote: Counting objects: 36, done.
remote: Compressing objects: 100% (32/32), done.
remote: Total 36 (delta 8), reused 7 (delta 0), pack-reused 0
Receiving objects: 100% (36/36), 4.82 KiB | 0 bytes/s, done.
Resolving deltas: 100% (8/8), done.
Checking connectivity... done.
$ cd elviswxy/travis-test
$ git checkout -qf 246043653617d38fc948b999740cbb32b804f252
This job is running on container-based infrastructure, which does not allow use of 'sudo', setuid and setguid executables.
If you require sudo, add 'sudo: required' to your .travis.yml
See http://docs.travis-ci.com/user/workers/container-based-infrastructure/ for details.
0.01s$ source ~/virtualenv/python2.7/bin/activate
$ python --version
Python 2.7.9
$ pip --version
pip 6.0.7 from /home/travis/virtualenv/python2.7.9/lib/python2.7/site-packages (python 2.7)
Could not locate requirements.txt. Override the install: key in your .travis.yml to install dependencies.
0.02s$ python helloworld.py
Hello, World!
The command "python helloworld.py" exited with 0.
Done. Your build exited with 0.
```
# Set the build logo.
你可以在respository的README.md文件中加入build状态图标。方法是在在该文件中加入 
```
[![Build Status](https://travis-ci.org/[YOUR_GITHUB_USERNAME]/[YOUR_PROJECT_NAME].png)](https://travis-ci.org/[YOUR_GITHUB_USERNAME]/[YOUR_PROJECT_NAME])
```
