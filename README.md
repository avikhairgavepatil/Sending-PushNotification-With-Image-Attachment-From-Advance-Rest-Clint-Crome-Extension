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


in ios swift 

in service.extension Class file 


import UserNotifications

class NotificationService: UNNotificationServiceExtension {
    
    let imageKey = AnyHashable("gcm.notification.url")
    
    var contentHandler: ((UNNotificationContent) -> Void)?
    var bestAttemptContent: UNMutableNotificationContent?
    
    override func didReceive(_ request: UNNotificationRequest, withContentHandler contentHandler: @escaping (UNNotificationContent) -> Void) {
        self.contentHandler = contentHandler
        bestAttemptContent = (request.content.mutableCopy() as? UNMutableNotificationContent)
       // let userInfo : [AnyHashable: Any] = response.notification.request.content.userInfo
        if let imageUrl = request.content.userInfo[imageKey] as? String {
            
            
            let session = URLSession.shared
            
            
            
            
            let url = URL(string: imageUrl)!
            
            
            
            let task = session.dataTask(with: url) { (data, response, err) in
                
                if let data = data {
                    do {
                        let writePath = URL(fileURLWithPath: NSTemporaryDirectory()).appendingPathComponent("push.png")
                        try data.write(to: writePath)
                        
                        if let bestAttemptContent = self.bestAttemptContent {
                            let attachment = try UNNotificationAttachment(identifier: "nnsnodnb_demo", url: writePath, options: nil)
                            bestAttemptContent.attachments = [attachment]
                            contentHandler(bestAttemptContent)
                        }
                    } catch let error as NSError {
                        print(error.localizedDescription)
                    
                        if let bestAttemptContent = self.bestAttemptContent {
                            contentHandler(bestAttemptContent)
                        }
                    }
                }
            }
            task.resume()
            
        }
            
else {
            if let bestAttemptContent = bestAttemptContent {
                contentHandler(bestAttemptContent)
            }
        }
    }
    
    override func serviceExtensionTimeWillExpire() {
        if let contentHandler = contentHandler, let bestAttemptContent =  bestAttemptContent {
            contentHandler(bestAttemptContent)
        }
    }
}


