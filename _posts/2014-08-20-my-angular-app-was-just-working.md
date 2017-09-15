---
layout: post
title: My Angular App is Broken after Upgrading to the Latest Beta
excerpt: 
tags: 
comments: true
---

##Introduction
I have been experimenting with AngularJS for a couple of months. After upgrading to 1.3.0-beta.18, I noticed the following code didn't work. I was previously using the latest stable build which is 1.2.22 as shown below:  

####The HTML File 

    <!DOCTYPE html>
    <html ng-app="">
    
    <head>
      <!--Works with latest Stable Build-->
      <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.22/angular.min.js"></script>
    
      <!--Does not work with Latest Beta-->
      <!--UNCOMMENT ME! <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.0-beta.18/angular.min.js"></script>-->
    
    
      <script src="script.js"></script>
    </head>
    
    <body ng-controller="MainController">
      <h1>Angular Playground</h1>
      {{message}}
      <br />Total Length: {{message.length}}
    </body>
    
    </html>

####The JavaScript File

    var MainController = function($scope) {
        $scope.message = "Hello, Michael";
    };


Using 1.2.22, the following is displayed in the browser: 

> Hello, Michael  
> Total Length: 14

However, if I use 1.3.0-beta.18, then I get the following error: 

> Error: [ng:areq] Argument 'MainController' is not a function, got undefined

And the page returns the following: 

> {{message}}  
> Total Length: {{message.length}}

####The Fix
After a lot of digging, I found several other had asked this question and it turns out that the answer is that with 1.3.x, you can't declare a global constructor and use it with ng-controller as I was doing before. You have to create an angular module and add MainController as a controller as shown below: 

    (function(angular) {
    
        function MainController($scope) {
            $scope.message = "Hello, Michael";
        };
    
        angular.module("app", []).controller("MainController", ["$scope", MainController]);
    
    })(angular);

The only modification needed for the HTML page is to add the name of the angular module as shown below (where before I left it blank): 

    <html ng-app="app">

##Wrap-Up
It is kind of a bummer to know that so many [breaking changes](https://github.com/angular/angular.js/blob/master/CHANGELOG.md) are introduced in each version of Angular, but maybe that is just the nature of the beast. Anyways, I hope this post helped someone out there that was struggling like I was. 



