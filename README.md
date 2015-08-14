**Apache Cordova Church App**

This is used as the default app template to create Church App. This Mobile friendly design makes it easy for users to create a new Church App.

**Versions and Tags**

Sample app is built and tested with Cordova 5.0.0 and we only support Cordova version greater than 3.0 and above.



**Required reading**

Please see the Getting Started with Android for PhoneGap guide [here]
(http://cordova.apache.org/docs/en/5.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide), 
(http://cordova.apache.org/docs/en/5.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide).





###  **_App Controller_**  ##########

  |www| folder

i) index.html, templates(folder)

ii) js/app.js

iii)js/key.txt

iv) js/controller.js

## **_key.txt_** #############

Before login to the app create an app in the api to generate an app key (api_key). Place the app_key in the key.txt file for login else previous app will be executed.

$http({method: "GET", url:"http://build.myappbuilder.com/api/buttons.json", cache: false, params:{"api_key":localStorage.appkey}})

 .success(function(data, status){
 
 })

 .error(function(data, status) {

 }); 



localStorage.appkey : To maintain the Church app localStorage.appkey is needed. Generate an localStorage.appkey from the api in separate app.



## **_Login_** #############



Login controller inside the controller.js

API For User Sign In: **http://build.myappbuilder.com/api/login.json**

Code:

$scope.loginvalues={};

$scope.loginvalues.username="newuser";

$scope.loginvalues.password="passkey123";

  $http({method: "POST", url:"http://build.myappbuilder.com/api/login.json", cache: false, params:{"login":$scope.loginvalues.username,"password":$scope.loginvalues.password}})

     .success(function(data, status){

     })

     .error(function(data, status) {

     });                                       

Creator of the app can only be able to login as Admin.

                                     

## **_Home** #############



Home Page contains slider images and address of church.


API For Getting Menu and the content details: **http://build.myappbuilder.com/api/buttons.json**

Code:

 $http({method: "GET", url:"http://build.myappbuilder.com/api/buttons.json", cache: false, params:params:{'api_key':localStorage.appkey,'id':$rootScope.buttoncontent.id}})

 .success(function(data, status){

     })

     .error(function(data, status) {

     });  



To Create Menu or Button:

API for create new menu.

Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})
.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
   })
.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:

$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
})
   .error(function(data, status, headers, config) {
                                    
});   







To Create content and slider images in Home page use the following code, snippet in "sliderpagecreateCtrl" controller in controller.js.


Code:

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.slidervalues.title,"text":$scope.slidervalues.address, "additional_field":"Slider with address"}})

.success(function(data, status){
                            
cordova.exec(function(response){

}, function(error){
 
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "POST", { api_key: localStorage.appkey,id:$scope.currentelementid}]);
                            			 
})

.error(function(data, status) {
                          
                          
});




To Edit contents in Home page use the following code, snippet in  "sliderpageeditCtrl" controller in controller.js.


Code:

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.buttoncontent.elements[0].id,"title":$scope.updateslidervalues.title,"text":$scope.updateslidervalues.text}})
                   
.success(function(data, status, headers, config) {
                 
})

   .error(function(data, status, headers, config) {
                  
});



To Delete the slider image use the following code, snippet in "sliderpageeditCtrl" controller in controller.js.        


Code:

$.ajax({type: "DELETE",url:"http://build.myappbuilder.com/api/elements/images.json", data: {"api_key":localStorage.appkey,"element_id":$rootScope.buttoncontent.elements[0].id,"id":sliderid}, cache: false,success:function(response){
                                            
},

   error:function(error,status){
 
}

   });

## **_About_** #############

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {

 });



To Create Menu or Button:

API for Create New Menu or Button.

Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                          
})

.error(function(data, status, headers, config) {

});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})

.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
 });  



To Create About page: Before creating this you have to choose imageandtext template from our predifined set of templates.

The following code is used in imageandtextcreateCtrl controller in controller.js

Code:

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.imageandtextcreatevalues.title,"text":$scope.imageandtextcreatevalues.text, "additional_field":"Images and Text"}})
                   .success(function(data, status){
                            
                            
              
cordova.exec(function(response){
                                         
}, function(error){
                                         
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "POST", { api_key: localStorage.appkey,id:$scope.currentelementid}]);
                            
                            
})

.error(function(data, status) {
                          
                          
});



To Edit About page:

Here, you can edit text and image.

Code:

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.buttoncontent.elements[0].id,"title":$scope.updateimageandtextvalues.title,"text":$scope.updateimageandtextvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                           
                            

                            
                           
cordova.exec(function(response){
                                         

                                         
                                         
                                         
}, function(error){
                                     
                                       
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "PUT", { api_key: localStorage.appkey,element_id:$rootScope.buttoncontent.elements[0].id,id:$rootScope.buttoncontent.elements[0].images[0].id}]);

  })
  
.error(function(data, status, headers, config) {
                          
                          
                          
 });






## **_Ministry_** #############

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
 });



To Create Menu or Button:

API for Create New Menu or Button.

Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})

.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})
.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To Create About page, before creating this you have to choose "Image with Text" template from our predifined set of templates.

The following is coded in imageandtextcreateCtrl controller in controller.js

Code:

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.imageandtextcreatevalues.title,"text":$scope.imageandtextcreatevalues.text, "additional_field":"Images and Text"}})
                   .success(function(data, status){
                            
                            
                            
                            
cordova.exec(function(response){
                                         
}, function(error){
                                         
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "POST", { api_key: localStorage.appkey,id:$scope.currentelementid}]);
                            
                            
})

.error(function(data, status) {
                          
                          
});



To Edit About page:

Here, you can Edit Text and Image.

Code:

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.buttoncontent.elements[0].id,"title":$scope.updateimageandtextvalues.title,"text":$scope.updateimageandtextvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                           
                            

                            
                           
cordova.exec(function(response){
                                         
                                     
                                         
                                         
                          
}, function(error){
                                     
                                       
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "PUT", { api_key: localStorage.appkey,element_id:$rootScope.buttoncontent.elements[0].id,id:$rootScope.buttoncontent.elements[0].images[0].id}]);
                            
                            
                            
                            
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});






## **_Sermons_** #############

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.

This is coded in videowithdescriptionpageCtrl controller in controller.js

Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})

.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})
.error(function(data, status, headers, config) {
                          
                          
 }); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To Create Sermons page, have to choose "Video with Description" from given Church Templates, use the following code, to create this template page.


The following is code used in videowithdescriptionpagecreateCtrl controller in controller.js

cordova.exec(function(response){
                                
                                
$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/tags.json", cache: false, params:{"api_key":localStorage.appkey,"id":response.id,"tags":"Videos with Description"}})

.success(function(data, status){
                                         
                          
                                         
})
.error(function(data, status) {
                                       
                                       
});
                                
}, 
function(e){alert(e);$ionicLoading.hide();}, "Thumbnail", "thumbnail",[localStorage.appkey,$rootScope.mainbuttonid,$scope.videowithdescriptioncreatevalues.title,$scope.videowithdescriptioncreatevalues.text,$('input[name="video"]').val(),"Nothumbnail", "post"])



To Edit Sermons page, use the following code, which is coded in videowithdescriptioneditpageCtrl controller in controller.js  


cordova.exec(function(response){
                                        
                                        
                                        
},
function(e){
                                        
}, "Thumbnail", "thumbnail",[localStorage.appkey,$rootScope.buttoncontent.elements[0].id,$scope.videowithdescriptioneditvalues.title,$scope.videowithdescriptioneditvalues.text,$('input[name="video"]').val(),"Nothumbnail", "put"])                            

## **_Image Gallery_** #############

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

$http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.

This is coded in imagespageCtrl controller in controller.js

Code:

$http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})
.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})
.error(function(data, status, headers, config) {
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To Create New Image use "Image Only Template" page, which is used in imagesaddpageCtrl controller in controller.js


cordova.exec(function(response){
                                         
                               
}, function(error){
                                        
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "POST", { api_key: localStorage.appkey,id:$rootScope.buttonforimages.elements[0].id}])    


Edit image, which is coded in imageseditpageCtrl controller in controller.js  

cordova.exec(function(response){
                                

}, function(error){
                                
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "PUT", { api_key: localStorage.appkey,element_id:$rootScope.buttonforimages.elements[0].id,id:$rootScope.imageselement.id}]); 



Delete Image, use the code in imagespageCtrl controller in controller.js
 
 $http({method: "DELETE", url:'http://build.myappbuilder.com/api/elements/images.json', cache: false, params:{'api_key':localStorage.appkey, 'element_id':buttonarray.elements[0].id,'id':elementarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                            
                                            
});                                                        			                                         

## **_Video_** #############

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

$http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})
.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.



Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
})
.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})
.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To Create Sermons page, have to choose "Video with Description" from given Church Templates, use the following code,.

You have to enter Page Title and Description and also have to choose video.


which is coded in videowithdescriptionpagecreateCtrl controller in controller.js

cordova.exec(function(response){
                                
                                
$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/tags.json", cache: false, params:{"api_key":localStorage.appkey,"id":response.id,"tags":"Videos with Description"}})

.success(function(data, status){
                                         
                          
                                         
})

.error(function(data, status) {
                                       
                                       
});
                                
}, 

function(e){

}, "Thumbnail", "thumbnail",[localStorage.appkey,$rootScope.mainbuttonid,$scope.videowithdescriptioncreatevalues.title,$scope.videowithdescriptioncreatevalues.text,$('input[name="video"]').val(),"Nothumbnail", "post"])



 To edit sermons page, use the following code,
 which is coded in videowithdescriptioneditpageCtrl controller in controller.js  


cordova.exec(function(response){
                                    
},
function(e){
                                        
}, "Thumbnail", "thumbnail",[localStorage.appkey,$rootScope.buttoncontent.elements[0].id,$scope.videowithdescriptioneditvalues.title,$scope.videowithdescriptioneditvalues.text,$('input[name="video"]').val(),"Nothumbnail", "put"]) 

## **_Program and Events_** #############

This is coded in textlistpageCtrl controller in controller.js

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.



Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
 })
 
.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})

                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To Create Program Events page, have to choose List Type from given church templates, use the following code, to create this template page.

which is coded in textlistpagecreateCtrl controller in controller.js

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.textlistcreatevalues.title,"text":$scope.textlistcreatevalues.text, "additional_field":"Text list"}})
.success(function(data, status){
                          
                            

})
.error(function(data, status) {
                          
                          
});



To Add Program event list content, use the following code,
which is coded in textlistaddpageCtrl controller in controller.js  


$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.buttoncontent.id,"title":$scope.textlistaddvalues.title,"text":$scope.textlistaddvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                            

                            
                            
})
.error(function(data, status, headers, config) {
                          
});


To Edit Program event list content, use the following code,
which is coded in textlisteditpageCtrl controller in controller.js

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.textlistelementcontent.id,"title":$scope.textlisteditvalues.title,"text":$scope.textlisteditvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
});

To Delete Program event list content, use the following code,
which is coded in textlistpageCtrl controller in controller.js

$http({method: "DELETE", url:'http://build.myappbuilder.com/api/elements.json', cache: false, params:{'api_key':localStorage.appkey, 'id':elementarray.id}})
             
                                     
.success(function(data, status, headers, config) {
                                              
                                              
                                              
})

.error(function(data, status, headers, config) {
                                            
                                           
                                            
});    






## **_Bible Quotes_** #############

This is coded in biblequotespageCtrl controller in controller.js

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})
.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.

This is coded in videowithdescriptionpageCtrl controller in controller.js

Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})

                   
.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  


To create Bible Quotes page, choose "List Type" from templates and use the following code, to create this template page.

which is coded in biblequotespagecreateCtrl controller in controller.js

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.biblequotescreatevalues.title,"text":$scope.biblequotescreatevalues.text, "additional_field":"Bible quotes"}})


.success(function(data, status){
                           
                            

})

.error(function(data, status) {
                          
                          
});



To add Bible Quotes list content, use the following code,
which is coded in biblequotesaddpageCtrl controller in controller.js  


  $http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.buttoncontent.id,"title":$scope.biblequotesaddvalues.title,"text":$scope.biblequotesaddvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                       
                            
                            
})

.error(function(data, status, headers, config) {
                         
                          
});


To Edit Bible Quotes list content, use the following code,
which is coded in biblequoteseditpageCtrl controller in controller.js

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.biblequoteselementcontent.id,"title":$scope.biblequoteseditvalues.title,"text":$scope.biblequoteseditvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
               
                            
})

.error(function(data, status, headers, config) {
                          
                          
});

To delete Bible Quotes list content, use the following code,
which is coded in biblequotespageCtrl controller in controller.js

$http({method: "DELETE", url:'http://build.myappbuilder.com/api/elements.json', cache: false, params:{'api_key':localStorage.appkey, 'id':elementarray.id}})
  
                                     
.success(function(data, status, headers, config) {
                                              
                                              
                                              
})

.error(function(data, status, headers, config) {
                                            
                                           
                                            
});      



## **_Our Ministries_** #############

This is coded in imageswithdescriptionlistpageCtrl controller in controller.js

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.



Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
 })
.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To create Our ministries page , have to choose Images with Description in List from given church templates, use the following code, to create this template page.

which is coded in imageswithdescriptionpagecreateCtrl controller in controller.js

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.imagewithdescriptioncreatevalues.title,"text":$scope.imagewithdescriptioncreatevalues.text, "additional_field":"Images with Description in List"}})

.success(function(data, status){
                            
cordova.exec(function(response){

}, function(error){
                                         
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "POST", { api_key: localStorage.appkey,id:$scope.currentelementid}]);
                            
                            
})

.error(function(data, status) {
                          
});



To add Our Ministries  content, use the following code,
which is coded in imageswithdescriptionlistpageaddCtrl controller in controller.js  


$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.imagewithdescriptionaddvalues.title,"text":$scope.imagewithdescriptionaddvalues.text}})
.success(function(data, status){
                            
cordova.exec(function(response){
                                         

}, function(error){
                                         
}, "ImageCompress", "imageCompress", ["370", "280", "image", $scope.image, "http://build.myappbuilder.com/api/elements/images.json?", "POST", { api_key: localStorage.appkey,id:$scope.currentelementid}]);
                            
                            
})

.error(function(data, status) {
                          
                          
                          });


To edit Our Ministries  content, use the following code,
  which is coded in imageswithdescriptionlistpageeditCtrl controller in controller.js

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.textlistelementcontent.id,"title":$scope.imagewithdescriptioneditvalues.title,"text":$scope.imagewithdescriptioneditvalues.text}})
.success(function(data, status){
                            
        

})

.error(function(data, status) {
                          
                          });

To delete Our Ministries content, use the following code,
which is coded in imageswithdescriptionlistpageCtrl controller in controller.js

$http({method: "DELETE", url:'http://build.myappbuilder.com/api/elements.json', cache: false, params:{'api_key':localStorage.appkey, 'id':elementarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                              
                                              
})

.error(function(data, status, headers, config) {
                                            
                                           
                                            
});



## **_FAQ_** #############

This is coded in textlistpageCtrl controller in controller.js

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.

This is coded in videowithdescriptionpageCtrl controller in controller.js

Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})

.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  



To create FAQ page , have to choose List Type from given church templates, use the following code, to create this template page.


which is coded in textlistpagecreateCtrl controller in controller.js

$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.mainbuttonid,"title":$scope.textlistcreatevalues.title,"text":$scope.textlistcreatevalues.text, "additional_field":"Text list"}})

.success(function(data, status){
                          
                            

})

.error(function(data, status) {
                          
                          
});



To add FAQ list content, use the following code,
which is coded in textlistaddpageCtrl controller in controller.js  


$http({method: "POST", url:"http://build.myappbuilder.com/api/elements/create_default.json", cache: false, params:{"api_key":localStorage.appkey,"button_id":$rootScope.buttoncontent.id,"title":$scope.textlistaddvalues.title,"text":$scope.textlistaddvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                            

                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
});


To edit FAQ list content, use the following code,
which is coded in textlisteditpageCtrl controller in controller.js

$http({method: "PUT", url:"http://build.myappbuilder.com/api/elements/update_default.json", cache: false, params:{"api_key":localStorage.appkey,"id":$rootScope.textlistelementcontent.id,"title":$scope.textlisteditvalues.title,"text":$scope.textlisteditvalues.text}})
                   
.success(function(data, status, headers, config) {
                            
                            
                     
                            
})

.error(function(data, status, headers, config) {
                          
                          
});

To delete FAQ list content, use the following code,
which is coded in textlistpageCtrl controller in controller.js

$http({method: "DELETE", url:'http://build.myappbuilder.com/api/elements.json', cache: false, params:{'api_key':localStorage.appkey, 'id':elementarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                              
                                              
})

.error(function(data, status, headers, config) {
                                            
                                           
                                            
});                                             


## **_Donations_** #############

This is coded in donationpageCtrl controller in controller.js

API For Getting the menu list : **http://build.myappbuilder.com/api/buttons.json**

Code:

  

 $http({method: "GET", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey}})
                   
.success(function(data, status, headers, config) {
                            
                            
})

.error(function(data, status, headers, config) {
                          
                          
                          
});



To Create Menu or Button:

API for Create New Menu or Button.



Code:

 $http({method: "POST", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"title":$scope.buttoncreatevalues.title,"image":"http://s3.amazonaws.com/iPhoneBooks/user/buttons/original/688.png"}})
                   
.success(function(data, status, headers, config) {
                            
                            
                            
})

.error(function(data, status, headers, config) {
                          
                    
});  

To Edit Menu or Button: 

API for Edit Menu or Button.

	Code:


$http({method: "PUT", url:"http://build.myappbuilder.com/api/buttons/via_url.json", cache: false, params:{"api_key":localStorage.appkey,"id":$scope.buttoneditvalues.buttonid,"title":$scope.buttoneditvalues.title}})
                   
.success(function(data, status, headers, config) {
                            
                   
                            
})

.error(function(data, status, headers, config) {
                          
                          
}); 


To Delete Menu or Button: 

API for Delete Menu or Button.

Code:


$http({method: "DELETE", url:'http://build.myappbuilder.com/api/buttons.json', cache: false, params:{'api_key':localStorage.appkey, 'id':buttonarray.id}})
                                     
.success(function(data, status, headers, config) {
                                              
                                             
                                              
})

.error(function(data, status, headers, config) {
                                            
                                         
                                            
});  


Donation payment

Stripe.setPublishableKey('pk_live_skZ8mxm9gORrvB7qNVXCSRiQ');  


$http({method: "GET", url:'http://nuatransmedia.com/song_app/church_stripe/charge.php', cache: false, params:{'token':$scope.stripeToken,'amount':$scope.totalAmount,'mail':mail}})
 
.success(function(data, status, headers, config) {
                      
                      
                      
})

.error(function(data, status, headers, config) {
             		
});
                                         

**For API references visit - ****http://build.myappbuilder.com/api**