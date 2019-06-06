# These are projects for 'Angular Zero to Hero', an excellent course by DanWahlin.
## Project1:

This project provides an introductory look at key features available in ES6/ES2015 which are important given that TypeScript is a superset of ES6/ES2015 features. All of the Angular projects uses TypeScript so if you’re new to the TypeScript language or to what ES6/ES2015 offers I’d recommend learning those concepts first before diving into Angular concepts.

Note that some people call it ES6, some call it ES2015, which is why I’m listing both here. ES6 is the same as ES2015.A set of ECMAScript 2015 (also called ES6) examples as well as a Gulp file that converts them to ES5 using Babel.

To run the project:
1. Install Node.js from https://nodejs.org (latest LTS version is recommended)
     Run ```npm install``` at the root of the project in a command window.

2. Install the gulp package globally:
    ```npm install -g gulp```

3. Run gulp (from the root of the project) in the command window to transpile ES6/ES2015 code to ES5 (leave the window open since it watches for file changes)

4. Open another console window and run npm start to launch the browser.

## Project2:

ES6/ES2015 modules play an important role in Angular (v2 or higher) applications so learning the basics about how modules work, how a module loader is configured, etc. is very important if you want to build Angular applications. This project provides a simple starter example of getting started with modules and the SystemJS module loader.
What is a module loader? Browser’s don’t support ES6/ES2015 modules quite yet so a “polyfill” script is needed to add-in the missing functionality. SystemJS is one of several module loaders out there that can be used to work with modules in browsers.

To run the project:
1. Install the gulp packages.
    ```npm install gulp -g```

2. Install the local packages for this demo.
    ```npm install```

3. Run Gulp:
    gulp

4. Run the server, launch the browser, and transpile the ES6 to ES5 using Babel
    npm start

#### Details
The source code is located in the js folder and written in ES6/ES2015. We use gulp to transpile to ES5 using Babel. The gulp command runs the default Gulp task which transpiles the code and puts it in the dist folder and then watches for more changes. If you change the source, it will transpile again.

When you launch index.html (via npm start), SystemJS kicks in and looks for config.js for its settings. We tell SystemJS that the base URL for the code is in /dist. This is important so all import statements that were written assuming relative pathing in the src folder will still work. Finally, we tell SystemJS that import statements by default should assume they end with .js. This is accomplished by setting defaultExtension to js. See the code below for an example.
```
System.config({
    map: {
      main: 'dist' //Map "main" to the "dist" folder
    },
    packages: {
      //Define settings for loading files in "dist"
      dist: {
        main: 'main.js',
        format: 'system',
        defaultExtension: 'js'
      }
    }
});
```
We can now import the main starting module (main.js) like this:

System.import('main');
Now SystemJS gets /dist/main.js which in turn imports car and truck. Each of those import auto and extend it. SystemJS knows that the base URL is /dist and to assume an extension of .js, so it really gets /dist/car.js and /dist/truck.js which in turn get /dist/auto.js.