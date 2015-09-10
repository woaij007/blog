title: Start ionic with API Demo
date: 2015-08-10 15:58:04
tags:
- Ionic
- API
- Instagram
categories: Ionic
---

Today I am going to build my first ionic project with Instagram API. Because it's easier to just get data from API rather than SQLite or local storage. 

## Create a blank Ionic project
### Install Ionic
Ionic is a framework based on [Node.js](https://nodejs.org/). Make sure you already have installed Node.js. 
``` bash
$ npm install -g cordova ionic
```
*Follow the [Android](http://cordova.apache.org/docs/en/3.3.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide) and [iOS](http://cordova.apache.org/docs/en/3.3.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide) platform guides to install platform dependencies you need.*
<!--more-->
### Start a project
``` bash
$ ionic start myApp blank
```
Ionic provide ready-made app templates as `tabs` and `sidemenu`, here I just started a `blank` one.

### Run your app
``` bash
$ cd myApp
$ ionic serve
```
Here I just run the app use Cordova directly. Later in another article I will write how to build an iOS app using Ionic.

Visit [localhost:8100](localhost:8100), you can see the page as below. In chrome browser you can use [Device Mode & Mobile Emulation](https://developer.chrome.com/devtools/docs/device-mode) to make the web just like an app in iPhone 6.
![](/img/blank_app.png)

## Get Instagram API
In order to use Instagram API in our app, we need to learn how to use it first.
### Register Your Application
Visit [API - Instagram](https://instagram.com/developer/) and log in with your Instagram account. If you don't have one yet, download Instagram app from App Store or Google Play store in your cellphone and create a new account.

After you logged in to [API - Instagram](https://instagram.com/developer/), you need to clike `Register Your Application` to register. After you done, you will get to a page like below, where you can get the information needed to get `access_token` for your API request.
![](/img/client_info.png)

### Use API Console
Click the `API Console` side bar to test making request to Instagram API. Select **Service** to `GET users/{user-id}/media/recent` and **Authentication** to `OAuth 2`. This API let you access to an Instagram user's recent media posts by its `user-id`.

For example, I want to know Taylor Swift's recent posts. I will go [Lookup Your Instagram User ID](http://jelled.com/instagram/lookup-user-id#) page, type in `taylorswift`, which is Taylor Swift's Instagram user name to get her `user-id` is `11830955` as below.
![](/img/user_id.png)

Back to API Console, click `Template`, input the `user-id`, and click `Send`. We will see our request and response as below.
![](/img/request_response.png)
Here we get the whole request is 
``` bash
https://api.instagram.com/v1/users/11830955/media/recent?access_token=1438541261.1fb234f.a3c0b2474c3447b2b3ecdbcd97244ac6
```
Now we are good to use this in our Ionic app.

## Build the API demo
### Use Card Images CSS
Ionic has many CSS components on [CSS Components](http://ionicframework.com/docs/components). Here we choose [Card Images](http://ionicframework.com/docs/components/#card-images) to show Taylor Swift's recent Instagram posts in our app.

Copy the following code into '/myApp/www/index.html' between `<ion-content>` and `</ion-content>`. 
``` bash
<div class="list card">

  <div class="item item-avatar">
    <img src="avatar.jpg">
    <h2>Pretty Hate Machine</h2>
    <p>Nine Inch Nails</p>
  </div>

  <div class="item item-image">
    <img src="cover.jpg">
  </div>

  <a class="item item-icon-left assertive" href="#">
    <i class="icon ion-music-note"></i>
    Start listening
  </a>

</div>
```
Run the app, and you will get:
![](/img/card_image.png)
### Get information from API
Now we need to get information from Taylor Swift's Instagram.

In `/myApp/www/js/app.js`, make change of line
``` bash
angular.module('starter', ['ionic'])
```
to be 
``` bash
var myapp = angular.module('starter', ['ionic'])
```
and add a controller named `ApiCtrl` by adding following codes:

``` bash
myapp.controller('ApiCtrl',function($scope, $http, $q) {

  $scope.init = function(){
    $scope.getImages()
    .then(function(res){
      // success
      console.log('Images: ',res)
      $scope.imageList = res.data;
    }, function(status){
      // err
      console.log('Error: ', status)
    })
  }

  $scope.getImages = function(){
    var defer = $q.defer();
    var url = "https://api.instagram.com/v1/users/11830955/media/recent?access_token=1438541261.1fb234f.a3c0b2474c3447b2b3ecdbcd97244ac6&callback=JSON_CALLBACK";
    $http.jsonp(url)
    .success(function(res){
      defer.resolve(res)
    })
    .error(function(status, err){
      defer.reject(status)
    })

    return defer.promise;
  }

  $scope.init();
});
```
In `index.html`, add control by changing 
``` bash
<ion-content>
```
to
``` bash
<ion-content ng-controller="ApiCtrl">
```
meaning in this content part, we will use data from `ApiCtrl` controller.

Run the app, we can get `res` as follow in chrome developer mode's `Console` tag. 
![](/img/res_data.png)
This is because we have line 
``` bash
console.log('Images: ',res)
```
in our controller to store the response from our API request as a json string.

### Put data in our UI
Now we can sort the data we need from `Images` and put them in the right place of our app's user interface.
``` bash
<body ng-app="starter">

    <ion-pane>
      <ion-header-bar class="bar-stable">
        <h1 class="title">Taylor Swift's Instagram</h1>
      </ion-header-bar>
      <ion-content ng-controller="ApiCtrl">
        <div class="list card" data-ng-repeat="image in imageList" >

          <div class="item item-avatar">
            <img ng-src="{{image.caption.from.profile_picture}}">
            <h2>{{image.caption.from.username}}</h2>
            <p>{{image.caption.from.full_name}}</p>
          </div>

          <div class="item item-image">
            <img data-ng-src="{{image.images.standard_resolution.url}}">
          </div>

          <a class="item item-icon-left assertive" data-ng-href="{{image.link}}">
            <i class="icon ion-android-send"></i>
            Visit Original Post
          </a>

        </div>
      </ion-content>
    </ion-pane>
</body>
```
Here I changed the page title to `Taylor Swift's Instagram` and created a list to show all recent posts (actually it's 20 posts), each with a link to visit the original Instagram post.

Run the app, and it's [working](http://45.79.85.36:8100/)! 
![](/img/taylor_swift.png)