# Contact List Appp tutorial
 download and install from nodehodejs.org






Mean stack RESTful application tutorial



1. Git Bash install
2. download and install from nodehodejs.org
3. create server.js file 
4. download and install sublime text editor  (https://www.sublimetext.com/)
5. open server.js in this editor
6. go to c/nodeprojects folder
7. install express to this folder : npm install express 
8. type the following in server.js:

var express = require('express');
var app = express();

9. test if server works corectly:

app.get('/', function (req,res) {
 res.send("Hello world from server.js")
});
app.listen(3000);
console.log("Server running on port 3000");
10 set up html template
Delete :
app.get('/', function (req,res) {
 res.send("Hello world from server.js")
});
Type:
app.use(express.static(__dirname + "/public"));

11. create dir public
12. create index.html and add the following to the file:

<!DOCTYPE>
<html>
<head>
	<title>Contact List App</title>
</head>
<body>
<h1>Contact List App</h1>
</body>
</html>
13. restart the server, should update web page to the header "Contact List App"
14. Set up Angular.js in index.html
go to https://angularjs.org/
Copy https://ajax.googleapis.com/ajax/libs/angularjs/1.5.5/angular.min.js

15. test angular.js ( uopdate index.html:
add ng-app to the <html> tag
add <input ng-model="test>
{{test}} angular to way binding
refresh a browser, type anything in text box and see the same text on the right of the box


16. Set up bootstrap in the index.html
go to getbootstart.com  --> getting-started and copy 2 top links into head section of the html file:

<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">

<!-- Optional theme -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap-theme.min.css" integrity="sha384-fLW2N01lMqjakBkx3l/M9EahuwpSfeNvV63J5ezn3uZzapT0u7EYsXMjQV+0En5r" crossorigin="anonymous">

17.test bootstrap (refresh the browser-  see layout and font changes)
18. add to html for the layout of  the app:
-remove
 <input ng-model="test">
{{test}}

-add
<div class="container"
		<h1>Contact List App</h1>
	</div>
-add table

<table class="table">
			<thead>
				<tr>
					<th>Name</th>
					<th>Email</th>
					<th>Number</th>
				</tr>
			</thead>
		</table>

19. create a controller - interact betwwen  view and model with data )
add mg-controller="ApCtrl"> to div
add controllers foilder to the public folder
create controller.js file in controllers folder - to connect it to index.html file

add <script src="controllers/controller.js"></script>

open controller.js file
</body>


20. 
Fix for the newer angular version:
var myApp=angular.module('myApp', []);
myApp.controller('AppCtrl', ['$Scope','$http',
	function($scope, $http){
		console.log("Hello World from controller");


	}]);

21. create a dummy data

add to controller,js

 person1 = {
		name: 'Tim',
		email: 'tim@email.com',
		number: '(111) 111-1111'
    };
    person2 = {
		name: 'emily',
		email: 'emily@email2.com',
		number: '(222) 222-2222'
    };
    person3 = {
		name: 'John',
		email: 'john@email.com',
		number: '(333) 333-3333'
    };

add an array:
	var contactlist = [person1, person2, person3];



	
22. put a dummy data into the table in the index.html file
For this we are using $scope wich according to angularjs web site is the glue between 
application controller and the view ( in outr case it is html page)

add  

$scope.contactlist = contactlist;

so in html file we can use our array

add to the index.html the following under thead:

		   <tbody>
				<tr mg-repeat="contact in contactlist">
					<td>{{contact.name}}</td>
					<td>{{contact.email}}</td>
					<td>((contact.number}}</td>					
				</tr>
			</tbody>


23.

get dummy data from the server instead of the controller:

add 
$http and $http.get('/contactlist')

to the controller file

add to the server file:

app.get('/contactlist', function (req, res) {

console.log("I received a GET request")

});

/contactlist is a router...

copy dummy data from controller to the server.js

var contactlist = [
    person1= {
        name: 'Tim',
        email: 'tim@gmail.com',
        number:'(571) 426-1433'
    },

    person2 = {
        name:'Liam',
        email:'neason@taken2.com',
        number: '(777) 777-7777'
    },

    person3={
        name: 'Jessie',
        email:'jessie@vma.com',
        number: '(684) 426-1232'
    }
];
add this line:

 res.json(contactlist);
this line send data in a json format wich controller can use

and delete $scope line from the conroller

add this to the server.js:

$http.get('/contactlist').success(function(response) {
 	console.log("I got the data i requested");
 	$scope.contactlist = responce;
});


24 . Install MongoDB

from mongodb.com into c:\mongo

creqate 2 folders for the mongodb:

c:\data
c:\data\db

25.
run mongodb

open GITbash
go to c/mongo/bin
type ./mongod

should say in the buttom:

 data capture with directory 'C:/data/db/diagnostic.data'
2016-05-16T12:47:55.991-0400 I NETWORK  [initandlisten] waiting for connections on port 27017

26. create initial data for the app (practice)
open another gitbash prompt and go again tp the bin folder
go to c/mongo.bin

type:
./mongo

show dbs

use contactlist

db.contactlist.insert({name: 'Tom', email: 'tom@testemail.com', number: '(444) 444-4444'})


should see:

WriteResult({ "nInserted" : 1 })

to view the data type:

db.contactlist.find()
should see:

{ "_id" : ObjectId("573a00b7c748133f705070bf"), "name" : "Tom", "email" : "tom@testemail.com", "number" : "(444) 444-4444" }

type:
db.contactlist.find().pretty()  
return:
{
        "_id" : ObjectId("573a00b7c748133f705070bf"),
        "name" : "Tom",
        "email" : "tom@testemail.com",
        "number" : "(444) 444-4444"
}

add  2 more records at once use []:
db.contactlist.insert([{name: 'Tracy', email: 'tracy@testemail2.com', number:'(555) 555-5555'}, {name: 'Tucker', email; 'tucker@testemail3.com', number: '(777) 777-7777'}])
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 2,
        "nUpserted" : 0,
        "nMatched" : 0,
        "nModified" : 0,
        "nRemoved" : 0,
        "upserted" : [ ]

test it:
db.contactlist.find().pretty()
{
        "_id" : ObjectId("573a00b7c748133f705070bf"),
        "name" : "Tom",
        "email" : "tom@testemail.com",
        "number" : "(444) 444-4444"
}
{
        "_id" : ObjectId("573a0a83cbebfc8091d9cff9"),
        "name" : "Tracy",
        "email" : "tracy@testemail2.com",
        "number" : "(555) 555-5555"
}
{
        "_id" : ObjectId("573a0a83cbebfc8091d9cffa"),
        "name" : "Tucker",
        "email" : "tucker@testemail3.com",
        "number" : "(777) 777-7777"
}


27.use npm to install mongojs

npm install mongojs


28. require mongojs
type in server.js:

var mongojs =  require('mongojs');
var db = mongojs('contactlist', [contactlist]);

2 lines specify what db and collection will be used in app

29.get data from mongodb with GET request
and delete dummy data:
var contactlist = [
    person1= {
        name: 'Tim',
        email: 'tim@gmail.com',
        number:'(571) 426-1433'
    },

    person2 = {
        name:'Liam',
        email:'neason@taken2.com',
        number: '(777) 777-7777'
    },

    person3={
        name: 'Jessie',
        email:'jessie@vma.com',
        number: '(684) 426-1232'
    }
];
 res.json(contactlist);

write the following:

b.contactlist.find(function (err, docs){
	console.log(docs);
	res.json(docs);
}); 

testing by refreshing server and browser

30. prepare index.html t post into DB
Ad the following:
<th>Action</th>

and 


<tr>
					<td><input class=form-control" ng-model="
					contact.name"></td>
					<td><input class="form-control" ng-model="contact.email"></td>
					<td><input class="form-control" ng-model="contact.number"></td>
					<td><button class="btn btn-primary" ng-click="addContact()">Add Contact</button></td>
				</tr>

31. define and test addContact function:
update controller file.

add 
$scope.addContact = function() {
   		console.log($scope.contact);
   }

refresh the console, should see a new record in a console

32. send input data from input boxes to the server.
add to the controller file

$http.post('/contactlist', $scope.contact);

add to the server file:
app.post('/contactlist', function (req, res) {
  console.log(req.body);
});

now we need to install body parser:

nmp install body-parser
add to server file:

var bodyParser = require('body-parser');

app.use(bodyParser.json());
refersh server and console

33. insert input data into mongodb

in serverjs:

db.contactlist.insert(req.body, function(err, doc) {
  	 

	res.json();
  };


34. 


add to the controller file  to chek if controller received a new data from the database:


$http.post('/contactlist', $scope.contact).success(function(response) { 
   		console.log(response);
   });

refresh server and browser

type in input box
data is inserted but not refreshed in the table
in controller file:

var refresh = function() {
$http.get('/contactlist').success(function(response) {
 	console.log("I got the data i requested");
 	$scope.contactlist = response;
 	$scope.contact = ""
});

refresh();
$scope.addContact = function() {
   		console.log($scope.contact);
   		$http.post('/contactlist', $scope.contact).success(function(response){
   			console.log(response);
   			refresh();
   		});
   };
test by refreshing server and console


delete and edit contact list with data from the database:

35. add remove button:


<td><button class="btn btn-danger" ng-click="remove					(contact._id)">Remove</button></td>
test by refreshing browser

36.

Add this function to the controller file:

$scope.remove = function(id) {
	console.log(id);
};
test by refreshing server and click o one remove button..and see id in a console 

37 , 38. send http request to the server and delete


in controller:

$scope.remove = function(id){
   console.log(id);
   $http.delete('/contactlist/'+id).success(function(response){
    
    refresh();
   });?
	

in server file:

app.delete('/contactlist/:id', function (req, res){
	var id = req.params.id;
	console.log(id);
	db.contactlist.remove({_id: mongojs.ObjectId(id)}, function (err, doc){
		res.json(doc);
	});


test by refereshing server and console

39. PUT request wich modify data in the table

add edit btn and upate btn
td><button class="btn btn-warning" ng-click="edit(contact._id,contact)">Edit</button></td>	
<td><button class="btn btn-info" ng-click="update()">Update</button></td>

test by refreshing a browser ...

40. Define an edit function

in controller add:

$scope.edit = function(id){
	console.log(id);
	$http.get('/contactlist/'+id).success(function(response){
  
   });?

in server file add

app.get('/contactlist/:id', function (req, res){
	var id = req.params.id;
	console.log(id);
	db.contactlist.findOne({_id: mongojs.ObjectId(id)}, function (err, doc){
		res.json(doc);
	});

$scope.update = function () {
	console.log($scope.contact,_id);
};
 

in server add

app.put('/contactlist/:id', function (req, res){
	var id = req.params.id;
	console.log(req.body.name);
	db.contactlist.findAndModify({
		query: {_id: mongojs.ObjectId(id)},
		update: {$set: {name: req.body.name, email: req.body.email, number: req.body.number}},
		new: true
	}, function (err, doc) {
		res.json(doc);
	});
});

in controller;

$http.put('/contactlist/' + $scope.contact._id, $scope.contact).success(function(response){
		refresh();
	});

43. fix a glitch:
by adding "clear button

add to index.html:
&nbsp;&nbsp;<button class="btn btn-info" ng-click="deselect()">Clear</button></td>

incontroler file:
$scope.deselect = function() {
	$scope.contact = "";
}




