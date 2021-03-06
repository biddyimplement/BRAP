<strong><a href="#fn">Browser Recorder And Player (BRAP)</a> - An Introduction</strong> <br/>
Imagine you would like to have a tool that provides a programmatic way to record what users do in a browser (e.g. clicks, keystrokes, etc.) and later to replay their actions. Imagine this tool wouldn't be worried about the type of browser (e.g. firefox, chrome, IE) used for recording and playing such user activities. Would that not be very useful ?

Browser Recorder And Player (BRAP) is exactly a tool like that. It is an open-source Java package where you can decide what type of user actions you are interested in for recording and playing. BRAP is smart in detecting the page changes due to user interactions and thus is very useful when you want to record and play users interactions in multi-page settings.
BRAP uses the Selenium WebDriver and jQuery under the hood. As a result, it is browser independent. 

<strong>Getting Started</strong>
First of all, please create a directory (say BRAP) and make its structure as follows: <br/>
  BRAP<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|-- BRAP.jar<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--  drivers<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--chrome<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--  scripts<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--  BRAP.js<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|-- jquery.min.js<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|--  output<br/>
  <br />
As you can see, the folder BRAP contains 3 sub-folders (drivers, scripts and output) and a Jar file (BRAP.jar). See below how to generate BRAP.jar. The "driver" sub-folder should contain the selenium driver for browsers. In the example, "chrome" is the driver for the Chrome browser. If you want to use a different browser, please put the corresponding driver in this folder.  In the "scripts" directory, you can see BRAP.js and jquery.min.js. You can specify what types of actions you would like to record in BRAP.js. jquery.min.js is injected in the page so that the program (BRAP.jar) can use jQuery to record and play the interactions. The "output" folder holds the result files. </p>

<strong> How to generate BRAP.jar ?</strong>
You can use build.xml to generate BRAP.jar : <br>
&nbsp;&nbsp;&nbsp;#] ant create_run_jar 

<p>Below, you'll see the commands to record and play interactions. But before that, please make sure you have the folder structure as above and you have the right driver (e.g. recent driver) in the "driver" directory. <br/>
<br/>

<strong> How to record?</strong><br />
  java -jar BRAP.jar -record -browser chrome -browserBin drivers/chrome -oDir op -scriptsDir scripts -file record.int -genInfoFiles  -url http://money.msn.com
 
<u>Output: </u><br/>If the parameter values are correct, the command launches a browser. Then you can interact with the page (e.g. filling form values, pressing enter, etc.). The interaction file (like record.int) will be generated in the directory specified in oDir (like op).

<u>Parameters:</u> <br/>
-url <br/>
&nbsp;&nbsp;&nbsp;&nbsp; The URL to be loaded before the interaction recording starts. <br/>
-record <br/>
&nbsp;&nbsp;&nbsp;&nbsp; Indicates to record interactions <br/>
-browser <br/>
&nbsp;&nbsp;&nbsp;&nbsp; The type of browser you want to use. Currently, the options are: [chrome|firefox]<br/>
&nbsp;&nbsp;&nbsp;&nbsp; Default Value: chrome<br/>
-browserBin <br/>
&nbsp;&nbsp;&nbsp;&nbsp; The binary driver file for the chosen browser 
&nbsp;&nbsp;&nbsp;&nbsp; <br/>
&nbsp;&nbsp;&nbsp;&nbsp; Default Value: drivers/chrome<br/>
-profile <br/>
&nbsp;&nbsp;&nbsp;&nbsp; user profile file  name for the browser [optional]. <br/>
-port <br/>
&nbsp;&nbsp;&nbsp;&nbsp; Port number for the recorder <br/>
&nbsp;&nbsp;&nbsp;&nbsp; Default Value: 4444 <br/>
-oDir <br/>
&nbsp;&nbsp;&nbsp;&nbsp; The output directory 
<br/>&nbsp;&nbsp;&nbsp;&nbsp; Default Value: output<br/>
-scriptsDir <br/>
&nbsp;&nbsp;&nbsp;&nbsp; The directory containing the BRAP JavaScripts 
<br/>&nbsp;&nbsp;&nbsp;&nbsp; Default Value: scripts
-genInfoFiles 
&nbsp;&nbsp;&nbsp;&nbsp; If present, generates page information in addition to interaction files <br/>
-file
&nbsp;&nbsp;&nbsp;&nbsp; The file where interactions should be recorded
<br/> 
&nbsp;&nbsp;&nbsp;&nbsp; Default Value: null, which means you should provide the file name

<u>A simple example of a command is: </u><br />
  java -jar BRAP.jar -record -file record.int -url http://money.msn.com 
  
<strong>How to Replay Recorded Interactions </strong>? <br/>
  java -jar BRAP.jar -play -browser chrome -browserBin drivers/chrome -file op/record.int 
<u>Output: </u><br/>  
Given the correct parameters, this command launches the specified browser and plays the interactions present in the supplied interaction file. <br/>
<u>Parameters:</u> <br/>  
-play <br/>
&nbsp;&nbsp;&nbsp;&nbsp; Indicates to replay the interactions 
<br/>-file<br/>
&nbsp;&nbsp;&nbsp;&nbsp; The  file containing the  interactions to play
<br/> Other parameters (-profile, -browser, -browserBin) are same as for recording.

<u>A simple example of a command with default assumptions is: </u>
java -jar BRAP.jar -play -file output/record.int

<strong> Player Server</strong> <br/>
You can start a player in server mode and execute interactions one-by-one. As the player will be running as a server, you can send the interactions from different computer in the network. 
The server mode can be enabled by using -player option as follows: 
 
java -jar BRAP.jar -playerserver -port 8888

<u>Parameters: </u>  
Accepted parameters: -player, -profile, -browser, -browserBin and -port (default 8888). They can be specified as before. <br/>

<u>Output: </u> 
You will see a browser window with a blank page. Now you can send interactions (using java program) to the server at:
http://localhost:PORT/brap 
See brap.player.SampleClient.java for more details.      

<strong>LICENSE</strong> <br>
See the license file

<strong>ACKNOWLEDGEMENTS</strong><br/>
<a name="fn"></a>BRAP was developed mostly when the owner of this project was at AT&T Labs Research. Thanks to Dan Melamed, Amanda Stent, Hyuckchul Jung and Giuseppe Di Fabbrizio for the great ideas and suggestions. 

