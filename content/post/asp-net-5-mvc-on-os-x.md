+++
date = "2015-06-28T19:18:08+03:00"
draft = false
title = "ASP.NET 5 MVC on OS X"
tags = ["DOTNET", "ASPNET", "OSX"]
+++

**How to create, build and run [ASP.NET 5 MVC](http://www.asp.net/mvc/mvc5) web application on OS X**

![Visual Studio Code](/images/visual-studio-code.png)

Plan:

1. Install homebrew
2. Install ASP.NET 5 on OS X
3. Generate ASP.NET MVC project
4. Build web application
5. Run it

# Install Homebrew
```ruby
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

# Install ASP.NET 5 on OS X
```
$ brew tap aspnet/dnx
$ brew install dnvm
```

Now add `source dnvm.sh` to your /.bash_profile, ~/.bashrc or ~/.zshrc at the end of file

# Generate ASP.NET MVC project
Install [Node.js](https://nodejs.org) if you still don't have it
```
$ brew install node
```

Now install CLI tool for running [Yeoman](http://yeoman.io) generators
```
$ npm install -g yo
$ npm install -g generator-aspnet
```

Navigate to folder where you want to generate ASP.NET 5 Web application and run generator

```
$ yo aspnet
```

Specify app name and select `Web application`

# Build web application

ASP.NET 5 uses [Bower](http://bower.io) package manager
```
$ npm install -g bower
```

Restore all dependencies

```
$ dnu restore
```

Navigate to project root folder where `project.json` and run build

```
$ dnu build
```

# Run it

On OS X it's possible to run ASP.NET application using [Kestrel](https://github.com/aspnet/KestrelHttpServer)

```
$ dnx . kestrel
```

Open browser and navigate to `http://localhost:5001`

You'll get exception:
```
An unhandled exception occurred while processing the request.

IOException: kqueue() FileSystemWatcher has reached the maximum nunmber of files to watch.
```

This is caused by bug in Mono 4.0.1: https://bugzilla.xamarin.com/show_bug.cgi?id=28693

**WORKAROUND**:
Add `export MONO_MANAGED_WATCHER=false` to your /.bash_profile, ~/.bashrc or ~/.zshrc at the end of file

Re-run application `$ dnx . kestrel` and refresh page

Congratulations!
![ASP.NET 5 Web application on OS X](/images/aspnet5-osx.png)

Feel free to ask me any questions in the comments below.
