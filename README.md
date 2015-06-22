# travis-test

Installation travis

首先，使Travis CI通过github OAuth认证。

点击https://travis-ci.org/右上角的Sign in with GitHub按钮，输入自己的github账号和密码，并允许Travis CI的认证。

然后，激活GitHub Service Hook。

GitHub给用户提供了一个Service Hook接口,只要用户对host在github上的repository作用了一些action(比如push，pull)，就会触发相应的Service Hook。而Travis CI正是基于这个原理来trigger你的build。当你发起一个push操作时，就会trigger Travis CI的服务。

设置方法是访问Travis CI的profile，选择相应的repository打开Service Hook开关。

然后登陆你的github，访问具体的repository的Service Hook页面，确保设置了Travis CI Hook的github name和travis token。

Make sure you have at least Ruby 1.9.3 (2.0.0 recommended) installed.

Updating your Ruby

If you have an outdated Ruby version, you should use your package system or a Ruby Installer to install a recent Ruby.

Ubuntu:

$ sudo apt-get install python-software-properties
$ sudo apt-add-repository ppa:brightbox/ruby-ng
$ sudo apt-get update
$ sudo apt-get install ruby2.1 ruby-switch
$ sudo ruby-switch --set ruby2.1


Alternatively, you can use a Ruby version management tool such as rvm, rbenv or chruby. This is only recommended if you need to run multiple versions of Ruby.

You can of course always compile Ruby from source, though then you are left with the hassle of keeping it up to date and making sure that everything is set up properly.

Troubleshooting

Ubuntu

On certain versions of Ubuntu (e.g., 13.10), you need to install the corresponding -dev package in order to build the C extension on which travis gem depends.

If you updated to Ruby 2.1 as shown above:

$ sudo apt-get install ruby2.1-dev

You can check your Ruby version by running ruby -v:

$ ruby -v
ruby 2.0.0p195 (2013-05-14 revision 40734) [x86_64-darwin12.3.0]
Then run:

$ gem install travis -v 1.7.7 --no-rdoc --no-ri

if you meet a bug: Error: failed to build gem native extension

$ sudo apt-get install ruby2.1-dev
Now make sure everything is working:

$ travis version
1.7.7

Development Version

You can also install the development version via RubyGems:

$ sudo gem install travis --pre
We automatically publish a new development version after every successful build.

