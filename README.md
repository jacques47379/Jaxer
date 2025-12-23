Provides an update to mod_jaxer.so so it runs with a newer version of Apache Web Server 2-2-4.
Apache Web Server 2-2-4 has been built-in to replace the original Apache Web Server 2-2-2.
Source files for the new connector are included.
Although the labels of Apache22 remain for the purposes of keeping the directory structure the same.

The hyperlinks connecting the source viewer have been removed.
The Apache2-4Build folder contains an out-of-the-box version of Jaxer originally compiled for Windows.
Logging settings have been changed to run in development mode by default with verbose logging instead of production mode. Error messages are displayed at the top or in an alert box if the server side encounters an error.

Jaxer's strongest point is its ease of setup. Its a portable application within a ZIP folder by default. Unzip the ZIP folder to have a zero config, zero compile client and server model.
For a small project <500 lines of code, Jaxer has an advantage of being able to build an integrated client and server model within a single file. Although it is possible to spread out an application as a multi-page application.
The client side is generally written in standards based HTML, CSS, and vanilla Javascript. The server side is a bit rigid, and is primarily writen in an older style vanilla Javascript, references proprietary Jaxer APIs, and occasionally jQuery.
Jaxer comes up in forum discussions from time-to-time as a tool to build local intranets, native applications using a browser as a GUI, or as a platform to build a week-end project.

Although the Apache Web Server front-end is uptodate for 2025, the backend components remain as a headless version of Firefox 3 from 2006.
Some of the server's Javascript functions either work correctly, needs a specific workflow to achieve an expected result, or otherwise dosen't work and alternatives need to be found. 
For instance, Jaxer's synchronous XHR requests no longer work in modern browsers in 2025. However, asyncronous XHR commands written using Jaxer's proprietary .async command continues to work well between the client and server.
Web connectivity uses Firefox 3's XUL connections and SSL3 for HTTPS. Web scraping can still be performed on HTTP websites which don't require HTTPS handshakes.
However, modern authentication models such as TLS 1.3 for HTTPS are too modern for Firefox 3 to handle. The backend of the server would probably need to be upgraded from Firefox 3 to Palemoon 30 to retain the use of existing XUL connections and to add support for TLS 1.3.

Jaxer applications are accessible from a web browser if the server is started using the batch file, and if the project is placed in the Public folder.
A few example applications are included initially within the public folder.
By default Jaxer uses a singular SQLite database to handle all database communication between Jaxer projects within the public folder. This can be found in the local_jaxer/data/default folder.
DB Browser for SQLite can help expore this database to view and change its contents.
Make sure database tables in each project folder have a unique name or database overlaps will occur!
If a Jaxer project attempts to connect to a local file stored on the server, Jaxer always looks in the local_jaxer/data/default folder first. A few server files are included here as examples.
