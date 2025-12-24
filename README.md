Provides an update to mod_jaxer.so so it runs with a newer version of Apache Web Server 2-4.
Apache Web Server 2-4 has been built-in to replace the original Apache Web Server 2-2.
Source files for the new connector are included.
Although the labels of Apache22 remain for the purposes of keeping the directory structure the same.

The hyperlinks connecting the source viewer have been removed.
The Apache2-4Build folder contains an out-of-the-box version of Jaxer originally compiled for Windows.
Logging settings have been changed to run in development mode by default with verbose logging instead of production mode. Error messages are displayed at the top or in an alert box if the server side encounters an error.

Jaxer's strongest point is its ease of setup. Its a portable application within a ZIP folder by default. Unzip the ZIP folder to have a zero config, zero compile client and server model.
For a small project <500 lines of code, Jaxer has an advantage of being able to build an integrated client and server model within a single file. Although it is possible to spread out an application as a multi-page application.
The client side is generally written in standards based HTML, CSS, and vanilla Javascript. The server side is a bit rigid, and is primarily writen in an older style vanilla Javascript, references proprietary Jaxer APIs, and occasionally jQuery.
Jaxer comes up in forum discussions from time-to-time as a tool to build local intranets, native applications using a browser as a GUI, or as a platform to build a week-end project.

Although the Apache Web Server front-end is uptodate for 2025, the backend components remain as a headless version of Firefox 3 from 2008.
Some of the server's Javascript functions either work correctly, needs a specific workflow to achieve an expected result, or otherwise dosen't work and alternatives need to be found. 
For instance, Jaxer's synchronous XHR requests between client and server no longer work in modern browsers in 2025. However, asyncronous XHR commands written using Jaxer's proprietary .async command continues to work well between the client and server.
Web connectivity uses Firefox 3's XUL connections and SSL3 for HTTPS. Web scraping can still be performed on HTTP websites which don't require HTTPS handshakes.
However, modern authentication models such as TLS 1.3 for HTTPS are too modern for Firefox 3 to handle. The backend of the server would probably need to be upgraded from Firefox 3 to Palemoon 30 to retain the use of existing XUL connections and to add support for TLS 1.3.

Jaxer applications are accessible from a web browser if the server is started using the batch file, and if the project is placed in the Public folder.
A few example applications are included initially within the public folder.
By default Jaxer uses a singular SQLite database to handle all database communication between Jaxer projects within the public folder. This can be found in the local_jaxer/data/default folder.
DB Browser for SQLite can help expore this database to view and change its contents.
Make sure database tables in each project folder have a unique name or database overlaps will occur!
If a Jaxer project attempts to connect to a local file stored on the server, Jaxer always looks in the local_jaxer/data/default folder first. A few server files are included here as examples.


When a page is accessed by a client:
1. The body of the document is prepared.
2. The onserverload command (or relevant window function) calls one or more function is executed on the server. The server can initialise database files and inject HTML nodes into the body through server-side rendering.
3. The page is sent to the client to render. The server-side is disconnected from the DOM and can no longer unilaterally inject HTML nodes. The onload command (or relevant window function) is executed on the client. Jaxer set events are converted into in-line functions in the document body.

4.0 The Jaxer Ajax lifecycle starts. Architecturally, the Jaxer lifecycle involves an event driven sequence of tightly coupled "server actions" rather than an MVC framework or RESTful architecture.

4.1 An event listener in a client side script, a timer expires in a client side script, or an in-line function in the document body is triggered as an event. Onclick for instance.

4.2 The event typically triggers a function in a client side script. If only client side javascript is required, the event may finish at this point on the client side. If database results are required, one or more .async functions from the proprietary Jaxer API are called to send a request to a function in a server proxy script. The async function has 3 parts. The name of the function in a server proxy script to call, the name of the client side response function to direct the result, and one or more parameters to send to the function in the server proxy script.

4.3 The server proxy script function evaluates the request. This usually involves a database query at some point. The server proxy script function can call server script helper functions if required. The server proxy script function must return a single result which will be piped as the parameter to the client side response function defined in the original calling .async function on the client side. The returning result is usually in 1 of 3 forms: Its either a message/result, a database resultset, or a custom array.

4.3.1 Message/result is the simplest but can't return anything other than a single number/message or an error. It can't unpack multiple results or different types of error messages for instance from a single server request.

4.3.2 A moderately complex alternative is a database resultset. Drop/create a temporary database table making sure its not colliding with another database table of the same name on the server, and fill the temporary database table with multiple results and error messages if required. Execute a query on the temporary database table and get a database resultset in the form of an array. This resultset can be set as the returning object which will become the parameter of the client side response function.

4.3.3 The most complicated alternative is a custom array. A database resultset array could have extra rows added to it using the array push command. Alternatively, a new matrix/array could be built from scratch to minimise the overhead of a temporary database table. This custom array can be set as the returning object which will become the parameter of the client side response function.

4.4 The client side response function evaluates the contents of its parameter and performs various client side actions such as manipulating the dom, displaying alerts, changing the webpage, or if database results are required, performing one or more .async functions and the cycle continues.
