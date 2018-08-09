# Sending-PushNotification-With-Image-Attachment-From-Advance-Rest-Clint-Crome-Extension

Sending Firebase Push Notification With Imageurl 



Reference url = https://qiita.com/nnsnodnb/items/22b989abb8fcbad2e34d


//Sending notification from advanse rest clint//

    
    Url = “https://fcm.googleapis.com/fcm/send”.  

Method = “Post”



// Header Parameter



content-type :    application/json

authorization :key=Firebase Server Key


//



Body :=





{"to":"Device Token Key",

  "collapse_key": "score_update",

 "time_to_live": 108,

"delay_while_idle": false,

"data": {

"classname": "",

"weburl": ""

},

"notification": {

"body": "test\",

"title": "test1234",

  

"sound": "mysound.caf",

 "color": "#ffffff",

"priority": "high",

"mutable_content": true,

"content_available": true,

"url": "https://test.com/images/Offer20Offer1.png"

}

 

}


// From Backend Side payload like this


"{\"to\":\"Device Token Key"
   \"notification\" : {
       \"body\" : \"test",
       \"title\" : \" Do Make Money \",
       \"click_action\": \"helloworld\",
       \"icon\": \"notification_default\",
       \"sound\" : \"default\",
   \"priority\": \"high\",
       \"mutable_content\": true,
    \"badge\": 0,
      \"image_url\" : \"https://upload.wikimedia.org/wikipedia/commons/2/2c/Rotating_earth_%28large%29.gif\"
   }


}"

