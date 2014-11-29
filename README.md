#Shovel apps CMS 
### **Open Source mobile App Maker**.
[http://shovelapps.org](http://shovelapps.org)


**Shovel apps CMS** is a mobile oriented CMS that lets you create
mobile apps editing the content of your app in a CMS fashion.

Select an app **template** and modify the contents to suit your needs.

In Web Content Management Systems, the finalilty of the system is to  allow you
to dedicate to the system content and the final frontend is on the browser.


**Shovel apps CMS** makes it easy for you to create an Hybrid App starting from 
HTML templates and editing the content by yourself without the nagging of having to install
an entire Phonegap environment for yourself.

When your are done editing your app's contents, you  can **create Android binaries
 with one click and test it right away in your device.**

**tl;dr**. **Shovel apps CMS** is a CMS that compiles itself to a mobile binary

##Download

[Latest version](https://github.com/oskosk/shovelapps-cms/archive/latest.zip)


## Installation

###Requirements 

You need [NodeJS](http://nodejs.org/download/) installed to run **Shovel apps CMS**. 

* Download the latest version in this directory.

```
$ wget https://github.com/oskosk/shovelapps-cms/archive/latest.zip
$ cd ~/shovelapps-cms
```
* Unzip it and run it.
```
$ unzip shovelapps-cms-latest.zip
$ cd shovelapps-cms-latest/
$ ./start.sh
```



## Run and open your browser

```
$ cd shovelapps-cms-latest/
$ ./start.sh
```

Open your browser in `http://localhost:3000`


### CMS Configuration

All config is loaded from the `config/default.json` once the CMS is installed.





##Development

The CMS  is based on well known technologies from the nodejs world like
(express)[http://expressjs.com], (socket.io)[http://socket.io], JSON storage,
JSON based express sessions and JADE templates.


##Folder structure


```
├── config
│   └── default.json // The default config file. Generated by the installer
├── filestorage // All data is stored under this directory
├── lib // Shovelapps-cms core libraries
├── plugins // 
├── server.js  // this is the process that is lifted by the start scripts
├── start.sh  // Linux/OSX start script
├── start.bat  // Windows start batch script
├── templates
│   ├── admin
│   ├── bootstrap-3-jade
└── README.md
```

### About the CMS's storage

Users data, session data and screens data is stored locally in the filesystem.

### Templates

Templates are the base for an app. An hybrid app should respect the mobile OSs
standards and these is difficult starting from pure HTML and having to relay
on multiple tools and iterations in order for the app to have a design consistent
with its look & feel.

Shovel apps CMS templates offer a precise UI structure for designing a professional
app that is designed with the practics you may already use in web developmentw.

####About paths in templates

* Use relative paths in the templates in order to keep consistent with 
the final structure that the app will have inside phonegap


#### How to make a template

Templates are written in the [Jade](http://jade-lang.com/) language. 
*Jade allows you to write HTML code that is not bogus in terms of orphan tags.*

1. Create a directory  called `mytemplate` under the `templates` dir.
1. Start from an `index.jade`. Put all of your page there. For example,
download a responsive template from some bootstrap  theme providers for example. **Tip:** *If you want to try with your own HTML, convert it to JADE with [HTML to Jade converter](http://html2jade.aaron-powell.com/)*.
1. Create an assets folder under `templates/mytemplate`. ** All files in assets will be available at the `assets/` URL in your apps frontend**.

#### Recommendations about assets and libraries for your app

* Load phonegap.js
* Load cordova.js
* Recommend loading jQuery
* Recommend loading FastClick
* Plugins and templates are written in jade
* Jade offers tidinees to other developers and designers. When the user or 
  another developers will 
  rarely find basic nesting issues with HTML tags that often cause misalignments.


## Debugging

Shovel apps CMS uses the `debug` module and debugs under the namespace `"cms*"`.

So in order to see debug messages logged by **shovelapps CMS** run it like this

```
$ DEBUG='cms*' server.js
```
Or if you prefer, watch every module log with
```
$ DEBUG='*' server.js 
```

##Issues

[Report your issues with Shovel apps CMS here](http://github.com/shovelapps/issues).

##Libraries used

* jQuery
* socket.io
* FastClick
* medium-editor
 * MediumButton

##Plugins

Plugins extend **Shovel apps CMS**'s backend features or the frontend by using extra
scripts or whatever HTML you want for extending the core.

###File structure of a plugin

```
shovelapps-cms
└── plugins
     └── chat
        ├── chat.html
        └── index.js
```
###Required files

You need at least an `index.js` file inside the plugin directory.


####index.js

The file `index.js` is a regular `common.js` module. I.e. you write it
like any other module that is loaded by `var plugin  = require("plugin")`.
**Shovel apps CMS** will run that `index.js` like that on start. 

In fact, it will asumme the plugin exports a function (`module.exports = fucntionName`)
and calls it with 3 arguments that let you extend the CMS.

```
module.exports = myModuleInit;

function myModuleInit(app, server, sockets) {
  
}
```

#####Plugin exported function

The function exported by the `index.js` of a plugin received these 3 arguments

* **app: **. The express app object (i.e, the request handler by calling `express()` ). 
* **server: ** The server on which this plugin is being initialized
* **sockets: ** **Shovel apps CMS** creates three websockets for communicating 
with the **App frontend**, the **CMS Admin Panel** and **Shovel apps build Platform**.
The latter connection allows the CMS to build the app for you without worrying
about a Phonegap installation. 
*  * **socket.frontend**. A `socket.io` server for the default namespace (`/`).
*  * **socket.adminpanel**. A `socket.io` server to the  namespace (`/admin`).
*  * **socket.adminpanel**. A `socket.io` server to the  namespace (`/admin`).

The exported function will receive `app`, `server` and `sockets` parameters
in order for you to extend the CMS. *Remember, the cms backend is an express app*.

#License 

The MIT License (MIT)

Copyright (c) 2014 Shovelapps Inc. oscar@shovelapps.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
