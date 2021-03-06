

<H1><A NAME="SECTION04130000000000000000"></A>
   <A NAME="2788"></A>
  
<A NAME="sectionpractica:conversordetemperaturasconkarmaytravis"></A>
<BR>
Práctica: Conversor de Temperaturas con Karma y Travis
</H1>

<P>

<H4><A NAME="SECTION04130010000000000000">
Donde</A>
</H4>
  

Véase  la rama <code>karma</code> en el repositorio descrito en la sección
<A HREF="node9.html#parrafo:dondetemperatura">1.2</A>.
Esta rama no está disponible al alumno.

<P>

<H4><A NAME="SECTION04130020000000000000">
Requisitos</A>
</H4>
  

<P>

<UL>
<LI>Añada a la práctica de la temperatura los elementos necesarios para la ejecución de las pruebas mediante Karma.
</LI>
<LI>Añada integración contínua usando Travis (travis-ci.org)
</LI>
<LI>Añada el badge de Travis en el <code>README.md</code>
</LI>
<LI>Añada tareas en el <code>Gulpfile</code> para la ejecución de las pruebas mediante Karma.
</LI>
<LI>Añada (si no lo hizo en la práctica anterior) cubrimiento con blanket.
</LI>
</UL>

<P>
Lea

<UL>
<LI><A NAME="tex2html68"
  HREF="http://karma-runner.github.io/0.8/plus/travis.html">Karma Travis CI</A>.
</LI>
<LI>El capítulo 
<A NAME="tex2html69"
  HREF="http://nereida.deioc.ull.es/~lpp/perlexamples/">Integración Contínua: Travis</A>
de los apuntes de LPP
</LI>
<LI><A NAME="tex2html70"
  HREF="http://docs.travis-ci.com/user/languages/javascript-with-nodejs/">Travis CI: Building a Node.js project</A>
</LI>
</UL>

<P>

<H4><A NAME="SECTION04130030000000000000">
Karma</A>
</H4>
  

<P>

<H4><A NAME="SECTION04130040000000000000">
Karma: Como Funciona</A>
</H4>
  

<P>

<UL>
<LI><A NAME="3057"></A><SPAN  CLASS="textbf">Karma</SPAN> (See 
<A NAME="tex2html72"
  HREF="http://karma-runner.github.io/0.10/intro/installation.html">Karma installation</A>)
is essentially a tool which spawns a web server that executes source
code against test code for each of the browsers connected. 

<P>
</LI>
<LI>The results
for each test against each browser are examined and displayed via the
command line to the developer such that they can see which browsers and
tests passed or failed.

<P>
</LI>
<LI>A browser can be captured either
  
<UL>
<LI>manually, by visiting the URL where the Karma server is listening (typically <code>http://localhost:9876/</code>)
</LI>
<LI>or automatically by letting Karma know which browsers to start when Karma is run 
  
</LI>
</UL>
</LI>
</UL>

<P>

<UL>
<LI>Karma also watches all the files, specified within the configuration file,
and whenever any file changes, it triggers the test run by sending a
signal the testing server to inform all of the captured browsers to run
the test code again. 
</LI>
<LI>Each browser then loads the source files inside an
<code>IFrame</code><A NAME="tex2html71"
  HREF="footnode.html#foot3051"><SUP><SPAN CLASS="arabic">1</SPAN>.<SPAN CLASS="arabic">1</SPAN></SUP></A>, 
executes the tests and reports the results back to the server.
</LI>
<LI>The server collects the results from all of the captured browsers and presents them to the developer.
</LI>
</UL>

<P>

<H4><A NAME="SECTION04130050000000000000">
Karma: Videos</A>
</H4>
  

<UL>
<LI><A NAME="tex2html73"
  HREF="http://youtu.be/5mHjJ4xf_K0">JS.everywhere(Europe) 2012: Testacular, the Spectacular JavaScript Test Runner - Vojta Jína</A>
YouTube
</LI>
<LI><A NAME="tex2html74"
  HREF="https://egghead.io/lessons/unit-testing-introduction-to-karma">Introduction to Karma</A>
Screencast.
</LI>
<LI><A NAME="tex2html75"
  HREF="http://youtu.be/YG5DEzaQBIc">Google Test Automation Conference GTAC 2013: Karma - Test Runner for JavaScript</A>
Vojta Jína. YouTube
</LI>
</UL>

<P>

<H4><A NAME="SECTION04130060000000000000">
Karma: Opciones en Línea de Comandos</A>
</H4>
  

<PRE>
[~/srcPLgrado/mocha-chai-browser-demo(master)]$ karma --help
Karma - Spectacular Test Runner for JavaScript.

Usage:
  /usr/local/bin/karma &lt;command&gt;

Commands:
  start [&lt;configFile&gt;] [&lt;options&gt;] Start the server / do single run.
  init [&lt;configFile&gt;] Initialize a config file.
  run [&lt;options&gt;] [ -- &lt;clientArgs&gt;] Trigger a test run.
  completion Shell completion for karma.

Run --help with particular command to see its description and available options.

Options:
  --help     Print usage and options.
  --version  Print current version.
</PRE>

<P>

<H4><A NAME="SECTION04130070000000000000">
Karma: Generando el Fichero de Configuración</A>
</H4>
  

In order to serve us well, Karma needs to know about our project in
order to test it and this is done via a configuration file. 

<P>
The configuration file can be generated using <code>karma init</code>:
<PRE>
$ karma init my.conf.js

Which testing framework do you want to use ?
Press tab to list possible options. Enter to move to the next question.
&gt; jasmine
</PRE>

<P>
<PRE>
Do you want to use Require.js ?
This will add Require.js plugin.
Press tab to list possible options. Enter to move to the next question.
&gt; no
</PRE>

<P>
<A NAME="tex2html76"
  HREF="http://requirejs.org/">http://requirejs.org/</A>
<P>
<PRE>
Do you want to capture a browser automatically ?
Press tab to list possible options. Enter empty string to move to the next question.
&gt; Chrome
</PRE>

<P>
<PRE>
What is the location of your source and test files ?
You can use glob patterns, eg. "js/*.js" or "test/**/*Spec.js".
Enter empty string to move to the next question.
&gt; 

Should any of the files included by the previous patterns be excluded ?
You can use glob patterns, eg. "**/*.swp".
Enter empty string to move to the next question.


Do you want Karma to watch all the files and run the tests on change ?
Press tab to list possible options.
&gt; yes

Config file generated at "/Users/casiano/local/src/javascript/PLgrado/mocha-tutorial/karma.conf.js".
</PRE>

<P>
The configuration file can be written in CoffeeScript as well. In fact,
if you execute <code>karma init</code> with a <code>.coffee</code> filename extension, it will
generate a CoffeeScript file.

<P>
Of course, you can write the config file by hand or copy paste it from another project ;-)

<P>
<PRE>
[~/srcPLgrado/mocha-tutorial]$ cat karma.conf.js 
// Karma configuration
// Generated on Mon Jan 20 2014 16:21:22 GMT+0000 (WET)

module.exports = function(config) {
  config.set({

    // base path, that will be used to resolve files and exclude
    basePath: '',


    // frameworks to use
    frameworks: ['jasmine'],


    // list of files / patterns to load in the browser
    files: [
      
    ],


    // list of files to exclude
    exclude: [
      
    ],


    // test results reporter to use
    // possible values: 'dots', 'progress', 'junit', 'growl', 'coverage'
    reporters: ['progress'],


    // web server port
    port: 9876,


    // enable / disable colors in the output (reporters and logs)
    colors: true,


    // level of logging
    // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
    logLevel: config.LOG_INFO,


    // enable / disable watching file and executing tests whenever any file changes
    autoWatch: true,


    // Start these browsers, currently available:
    // - Chrome
    // - ChromeCanary
    // - Firefox
    // - Opera (has to be installed with `npm install karma-opera-launcher`)
    // - Safari (only Mac; has to be installed with `npm install karma-safari-launcher`)
    // - PhantomJS
    // - IE (only Windows; has to be installed with `npm install karma-ie-launcher`)
    browsers: ['Chrome', 'Firefox'],


    // If browser does not capture in given timeout [ms], kill it
    captureTimeout: 60000,


    // Continuous Integration mode
    // if true, it capture browsers, run tests and exit
    singleRun: false
  });
};
</PRE>

<P>

<H4><A NAME="SECTION04130080000000000000">
Arrancando Karma. Starting Karma</A>
</H4>
  

<P>
When starting Karma, the configuration file path can be passed in as the first argument.
By default, Karma will look for <code>karma.conf.js</code> in the current directory.
<PRE>
# Start Karma using your configuration
$ karma start my.conf.js
</PRE>

<P>
Some configurations, which are already present within the configuration
file, can be overridden by specifying the configuration as a command
line argument for when Karma is executed.
<PRE>
karma start karma-conf.js --command-one --command-two
</PRE>

<P>
<PRE>
[~/srcPLgrado/mocha-tutorial]$ karma start --help
Karma - Spectacular Test Runner for JavaScript.

START - Start the server / do a single run.

Usage:
  /usr/local/bin/karma start [&lt;configFile&gt;] [&lt;options&gt;]

Options:
  --port                &lt;integer&gt; Port where the server is running.                            
  --auto-watch          Auto watch source files and run on change.                             
  --no-auto-watch       Do not watch source files.                                             
  --log-level           &lt;disable | error | warn | info | debug&gt; Level of logging.              
  --colors              Use colors when reporting and printing logs.                           
  --no-colors           Do not use colors when reporting or printing logs.                     
  --reporters           List of reporters (available: dots, progress, junit, growl, coverage). 
  --browsers            List of browsers to start (eg. --browsers Chrome,ChromeCanary,Firefox).
  --capture-timeout     &lt;integer&gt; Kill browser if does not capture in given time [ms].         
  --single-run          Run the test when browsers captured and exit.                          
  --no-single-run       Disable single-run.                                                    
  --report-slower-than  &lt;integer&gt; Report tests that are slower than given time [ms].           
  --help                Print usage and options.
</PRE>

<P>

<H4><A NAME="SECTION04130090000000000000">
Using Karma with Mocha</A>
</H4>
  

To use Karma with Mocha
we need the karma-mocha adapter.

<P>
If we want to pass configuration options directly to mocha you can do this in the following way
<PRE>
// karma.conf.js
module.exports = function(config) {
  config.set({
    frameworks: ['mocha'],

    files: [
      '*.js'
    ],

    client: {
      mocha: {
        ui: 'tdd'
      }
    }
  });
};
</PRE>
(By default the <code>ui</code> is <code>bdd</code>).

<P>
Here is an example

<P>
<PRE>
[~/srcPLgrado/temperature(karma)]$ cat karma.conf.js 
// Karma configuration
// Generated on Thu Jan 29 2015 16:51:38 GMT+0000 (WET)

module.exports = function(config) {
  config.set({

    // base path, that will be used to resolve files and exclude
    basePath: '',

    // frameworks to use
    frameworks: ['mocha'],

    client: {
          mocha: {
            ui: 'tdd'
          }
    },

    preprocessors: {
          'tests/test.html': ['html2js']
    },


    // list of files / patterns to load in the browser
    files: [
      'tests/test.html',
      'tests/*.js',
      'temperature.js'
    ],


    // list of files to exclude
    exclude: [

    ],


    // test results reporter to use
    // possible values: 'dots', 'progress', 'junit', 'growl', 'coverage'
    reporters: ['progress'],


    // web server port
    port: 9876,


    // enable / disable colors in the output (reporters and logs)
    colors: true,


    // level of logging
    // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
    logLevel: config.LOG_INFO,


    // enable / disable watching file and executing tests whenever any file changes
    autoWatch: true,


    // Start these browsers, currently available:
    // - Chrome
    // - ChromeCanary
    // - Firefox
    // - Opera (has to be installed with `npm install karma-opera-launcher`)
    // - Safari (only Mac; has to be installed with `npm install karma-safari-launcher`)
    // - PhantomJS
    // - IE (only Windows; has to be installed with `npm install karma-ie-launcher`)
    browsers: [
               'Chrome',
               'Firefox',
               'PhantomJS',
               ],


    // If browser does not capture in given timeout [ms], kill it
    captureTimeout: 60000,


    // Continuous Integration mode
    // if true, it capture browsers, run tests and exit
    singleRun: false
  });
};
</PRE>
Another example can be found at
(<A NAME="tex2html77"
  HREF="https://github.com/crguezl/nathanuniversityexercisesPL/blob/master/scheem8/karma.conf.js">https://github.com/crguezl/nathanuniversityexercisesPL/blob/master/scheem8/karma.conf.js</A>).

<P>

<H4><A NAME="SECTION041300100000000000000">
Algunas dependencias para ejecutar Karma</A>
</H4>
  

De hecho, para poder usar Karma con los diferentes navegadores es necesario
instalar unos cuantos módulos. Vea este fragmento de <code>package.json</code>
<PRE>
 "devDependencies": {
    "chai": "*",
    "mocha": "*",
    "karma": "*",
    "karma-mocha": "*",
    "karma-html2js-preprocessor": "*",
    "karma-chrome-launcher": "*",
    "karma-firefox-launcher": "*",
    "karma-phantomjs-launcher": "*"
  },
</PRE>

<P>

<H4><A NAME="SECTION041300110000000000000">
Load HTML files with Karma</A>
</H4>
  

<P>
If you have one html file:
<PRE>
[~/srcPLgrado/karma/html]$ cat template.html 
&lt;div id="tpl"&gt;content of the template&lt;/div&gt;
</PRE>
which you want to load and then get all elements
from that html page in your test script,
you can use the <code>html2js</code> preprocessor, which basically converts
HTML files into JavaScript strings and include these files.
<PRE>
[~/srcPLgrado/karma/html]$ cat karma.conf.js 
module.exports = function(karma) {
  karma.configure({
    basePath: '',
    frameworks: ['jasmine'],
    files: [ '*.js', '*.html' ], 
    preprocessors: { '*.html': 'html2js' },
    ....
</PRE>
Then, you can access these strings in your test:
<PRE>
[~/srcPLgrado/karma/html]$ cat test.js 
describe('template', function() {
  it('should expose the templates to __html__', function() {
    document.body.innerHTML = __html__['template.html'];
    expect(document.getElementById('tpl')).toBeDefined();
  })
})
</PRE>

<P>
Preprocessors in Karma allow you to do some work with your files before they get served to the browser. The configuration of these happens in this block in the config file.
<PRE>
preprocessors = {
  '**/*.coffee': 'coffee',
  '**/*.html': 'html2js'
};
</PRE>
<H4><A NAME="SECTION041300120000000000000">
tests/tests.js usando Karma y Considerando el HTML</A>
</H4>
  

Por tanto modificamos nuestro fichero <code>tests/tests.js</code> como sigue:
<PRE>
[~/srcPLgrado/temperature(karma)]$ cat tests/tests.js 
var assert = chai.assert;

suite('temperature', function() {
    setup(function(){
      if (typeof __html__ !== 'undefined') {
          document.body.innerHTML = __html__['tests/test.html'];
          original = document.getElementById('original');
          converted = document.getElementById('converted');
      }
    });

    test('32F = 0C', function() {
        original.value = "32F";
        calculate();
        assert.deepEqual(converted.innerHTML, "0.0 Celsius");
    });
    test('45C = 113.0 Farenheit', function() {
        original.value = "45C";
        calculate();
        assert.deepEqual(converted.innerHTML, "113.0 Farenheit");
    });
    test('5X = error', function() {
        original.value = "5X";
        calculate();
        assert.match(converted.innerHTML, /ERROR/);
    });
});
</PRE>

<P>

<H4><A NAME="SECTION041300130000000000000">
tests/test.html usando Karma y Considerando el HTML</A>
</H4>
  

El fichero <code>html</code> inicial también cambia, ya que Karma se encarga
de la carga de los ficheros HTML y de su pre-procesado:

<P>
<PRE>
[~/srcPLgrado/temperature(karma)]$ cat tests/test.html 
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Mocha&lt;/title&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;

  &lt;/head&gt;
  &lt;body&gt;
    &lt;div id="mocha"&gt;&lt;/div&gt;
    &lt;input id="original" placeholder="32F" size="50"&gt;
    &lt;span class="output" id="converted"&gt;&lt;/span&gt;

    &lt;script src="../temperature.js"&gt;&lt;/script&gt;
    &lt;script&gt;mocha.setup('tdd')&lt;/script&gt;
    &lt;script src="tests.js"&gt;&lt;/script&gt;

    &lt;script&gt;
      mocha.run();
    &lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;
</PRE>
Obsérvese que no cargamos <code>mocha</code>, etc porque son cargados por Karma (como especificamos en el fichero de configuración).

<P>

<H4><A NAME="SECTION041300140000000000000">
Karma y HTML: Véase</A>
</H4>
  

See 

<UL>
<LI><A NAME="tex2html78"
  HREF="http://stackoverflow.com/questions/18317693/load-html-files-with-karma">Load HTML files with Karma</A>
in StackOverflow.
</LI>
<LI><A NAME="tex2html79"
  HREF="https://github.com/karma-runner/karma-html2js-preprocessor">karma-html2js-preprocessor</A>
</LI>
</UL>

<P>

<H4><A NAME="SECTION041300150000000000000">
Karma y Gulp</A>
</H4>
  

<P>
Para automatizar la ejecución de las pruebas con <code>karma</code> y <code>gulp</code>
añadimos un par de tareas a nuestor <code>gulpfile</code>. Las tareas <code>test</code> y
<code>default</code>:

<P>
<PRE>
[~/srcPLgrado/temperature(karma)]$ cat gulpfile.js 
var gulp    = require('gulp'),
    gutil   = require('gulp-util'),
    uglify  = require('gulp-uglify'),
    concat  = require('gulp-concat');
var karma   = require('gulp-karma');
...

gulp.task('test', function() {
  // Be sure to return the stream
  return gulp.src([])
    .pipe(karma({
      configFile: 'karma.conf.js',
      action: 'run'
    }))
    .on('error', function(err) {
      // Make sure failed tests cause gulp to exit non-zero
      throw err;
    });
});

gulp.task('default', function() {
  gulp.src([])
    .pipe(karma({
      configFile: 'karma.conf.js',
      action: 'watch'
    }));
});
</PRE>

<P>

<H4><A NAME="SECTION041300160000000000000">
Karma y Travis</A>
</H4>
  

<P>
Véase
<A NAME="tex2html80"
  HREF="http://karma-runner.github.io/0.12/plus/travis.html">http://karma-runner.github.io/0.12/plus/travis.html</A>.

<P>

<UL>
<LI>Travis CI is a popular continuous integration service that integrates
with your Github repository to automatically run your tests when code
is pushed. 

<P>
</LI>
<LI>Integration is done by adding a simple YAML file to your
project root; Travis and Github take care of the rest. 

<P>
</LI>
<LI>Whenever tested,
the Travis results will appear in your Github pull requests and your
history will be available within their control panel. 

<P>
</LI>
<LI><B>Configure Travis</B>

<P>
Create a file in your project root called <code>.travis.yml</code> with the following YAML content:
<PRE>
language: node_js
node_js:
  - "0.10"
</PRE>
</LI>
<LI><B>Setup a Test Command</B>

<P>

<UL>
<LI>If you do not already have a <code>package.json</code> in your project root create one now. 

<P>
</LI>
<LI>Travis runs <code>npm test</code> to trigger your tests so this is where you tell Travis how to run your tests.
<PRE>
// ...snip...
'devDependencies': {
  'karma': '~0.12'
},
// ...snip...
'scripts': {
   'test': './node_modules/karma/bin/karma start --single-run --browsers PhantomJS'
}
// ...snip...
</PRE>
</LI>
<LI>Travis will run <code>npm install</code> before every suite so this is your
chance to specify any modules your app needs that Travis does not know
about like Karma.
</LI>
</UL>
</LI>
<LI><B>Configure Travis with Firefox</B>

<P>
Travis supports running a real browser (Firefox) with a virtual screen. Just update your <code>.travis.yml</code> to set up the virtual screen like this:
<PRE>
language: node_js
node_js:
  - "0.10"
before_script:
  - export DISPLAY=:99.0
  - sh -e /etc/init.d/xvfb start
</PRE>
And now, you can run your tests on Firefox, just change the <code>npm test</code> command to
<PRE>
karma start --browsers Firefox --single-run
</PRE>
</LI>
<LI>Si sólo se quiere testear una rama particular:
<PRE>
branches:
  only:
    - tests
</PRE>
</LI>
<LI><B>Notes</B>

<P>

<UL>
<LI>Travis' Node environment has very little available. If the startup process in Travis fails check for missing module information and be sure to add them to your <code>package.json</code> dependencies.
</LI>
<LI>Travis does not run in your local network so any code that attempts to connect to resources should be stubbed out using 
    <A NAME="tex2html81"
  HREF="https://github.com/flatiron/nock">Nock</A>
(Nock is an HTTP mocking and expectations library for Node.js).
</LI>
<LI>There are more options available to your <code>.travis.yml</code>, such as running scripts before the install or test run. There are hints in the Travis docs for GUI apps configuration.
    
</LI>
</UL>
</LI>
</UL>

<P>
