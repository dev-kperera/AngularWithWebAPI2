# AngularWithWebAPI2
Sample application created with Angular JS (version 1.5) front-end and ASP.NET Web API back-end.  

Simple scenario 
There are a list of book details which retrieves from the Web API and shown those in the front end using Angular JS. 
Architecture for the scenario 

•	Web browser request for page from the web server (eg: abc.com)
•	Web server will respond with html page which contains references to other contents such as scripts, styles and etc. Then after it will download contents as well
•	Angular activates and works as for user interactions. Since there is no binding with server directly, angular will call the Web API and get tasks done. 
Note: Other than Web API, we can also use Rails, NodeJS and etc.
Create the solution 
•	Create new project with ASP.NET Web API template 
•	Add new web site (Right clickAddNew Web site) to maintain our Angular front end. This will be better approach rather than maintaining the Angular within the Web API project. 
Architecture of Web API 
•	Client will request with the GET, POST and etc. with a valid URL  
•	Hits on the Web API Routing and redirects to specific controller 
•	After processed by business logic ‘action’ will respond client 
Some notes when working with Web API;
•	Routing and other action definitions are done in the WebApiConfig.cs (http://www.asp.net/web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api)
•	Web API Model  specifies data exposed by the API and defines data type which will be returned 
•	Web API repository  Place where contains logic for getting and saving data to the Model. Data can be obtained from ADO.NET, EF, JSON, XML or etc. 
•	Create controller as for the requirement with scaffolding 
After you done with above, run the Web API project and visit the “API” navigation. There you will find the URL for consume the REST service we have implemented upto now.

Angular $http
  •	Built in core functionality 
  •	Facilitate to consume web services asynchronously 
Angular $resource
  •	Requires “angular-resource”
  •	Build on top of $http and requires less code to communicate 
  
After integrating Angular $resource querying with the Web API. Need to run the project, but since there are two interdependent projects. We have to make following changes;
•	Select “Don’t open a page” on the start action of the Web API project properties 
•	On the solution properties set multiple projects startup and select your client and back end solutions

Note [Cross Origin Resource Sharing]:
If you get following error.. There is nothing to worry.. Issue is with the CORS (Cross Origin Resource Sharing). Which means we accessing the Web API by different Uri other than the request. In my case angular URL is “http://localhost:63084/” and accessing the “http://localhost:63084/api/Books”. 
XMLHttpRequest cannot load http://localhost:62776//api/Books. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:63084' is therefore not allowed access.
Solutions for above; 
•	Using the JSONP (passing “?jsonp=parseResponse” with the url)
•	Using CORS(this is the recommended way of doing and by W3C)
  o	Download the CORS using nugget package manager (Microsoft ASP.NET Web API 2.2)
  o	Add config.EnableCors(); to the WebApiConfig.cs
  o	Add [EnableCorsAttribute("http://localhost:63084/","*","*")] on top of your controller

Note [Serialization formatters]:
In some instances REST API object naming and Angular naming of the object may differ. In that instance you may use “Serialization formatters” to achieve this mapping.
