FORMAT: 1A
HOST: https://bluma.azurewebsites.net

# Bluma Messaging API Documentation

This is a quick, convenient and affordable way of sending SMS and Email messages both to managed and random contacts.

To try Bluma Messaging, complete the signup form and verify your account.

The base domain is : https://bluma.azurewebsites.net

## Expected Models (C#)
### Message Model
The expected message class model looks like this:
    
    public class Message {
    
        public long Id { get; set; }
        public MessageType Type { get; set; }
        public string SenderId { get; set; }
        public string Subject { get; set; }
        public string Message { get; set; }
        public string Recipients { get; set; }
        
    }

### Message Type Model
The expected message type enum looks like this:

    public enum MessageType{
    
        SMS,
        Email
    }

## Important Notes
* The sender id must not be more than 11 characters
* The message content must not be empty
* The message type must be SMS or Email

## How to generate an API Key
* Login  to the Bluma Portal
* Click on the settings dropdown and select subscriptions to open the subscriptions page
* Click on the refresh icon by the default subscription to generate a new API key
* Click on the details icon to open and copy your API key.


## Check Available Balance [/api/checkbalance]
### Check Balance [GET]
This api call returns an object that holds the available Email and SMS Balance for the active subscription.
+ Response 200 (application/json)

        {
            "total": 1,
            "message": "Successful",
            "success": true,
            "data": {
                "emailBalance": 123,
                "sMSBalance": 2048
            }
        }

## Send Bulk Messages [/api/sendmessages]

### Send Messages [POST]

This API is used to send bulk messages to a list of contacts. You can only send an SMS or Email message at a time.
The list of recipients should be concatenated into a long string with ",". Eg. "somemail@email.com,anothermail@email.com,yetanothermail@email.com" as the recipients for an email message, or "0201231231,0244121212,0234123122" as the recipients for an sms message.
The recipients can be of any considerable length.

+ Request (application/json)

    + Headers
        
            Authorization: Bearer youhavetoreplacethisstringwiththeapikeyofyoursubscription
        
    + Body
    
            {
                "type": "SMS",
                "senderId": "Bluma", 
                "subject": "Message Subject",
                "message": "this can contain any length of strings and  html elements and images",
                "recipients": "0244443322,0234234232,0203423422,055678945"
            }

+ Response 201 (application/json)
    
    + Body

            {
                "total": 1,
                "message": "Successful",
                "success": true,
                "data": null
            }
            
## Send Bulk SMS Messages [/api/sendsmsmessages]

### Send SMS Messages [POST]

This API is used to send bulk messages to a list of contacts. You can only send an SMS or Email message at a time.
The list of recipients should be concatenated into a long string with ",". Eg."0201231231,0244121212,0234123122".
The recipients can be of any considerable length.

+ Request (application/json)

    + Headers
        
            Authorization: Bearer youhavetoreplacethisstringwiththeapikeyofyoursubscription
        
    + Body
    
            {
                "type": "SMS",
                "senderId": "Bluma", 
                "subject": "Message Subject",
                "message": "this can contain any length of strings and  html elements and images",
                "recipients": "0244443322,0234234232,0203423422,055678945"
            }

+ Response 201 (application/json)
    
    + Body

            {
                "total": 1,
                "message": "Successful",
                "success": true,
                "data": null
            }
            
## Send Bulk Email Messages [/api/sendemailmessages]

### Send Email Messages [POST]

This API is used to send bulk email messages to a list of contacts. You can only send an SMS or Email message at a time.
The list of recipients should be concatenated into a long string with ",". Eg. "somemail@email.com,anothermail@email.com,yetanothermail@email.com".
The recipients can be of any considerable length.

+ Request (application/json)

    + Headers
        
            Authorization: Bearer youhavetoreplacethisstringwiththeapikeyofyoursubscription
        
    + Body
    
            {
                "senderId": "Bluma", 
                "subject": "Email Message Subject",
                "message": "this can contain any length of strings and  html elements and images",
                "recipients": "0244443322,0234234232,0203423422,055678945"
            }

+ Response 201 (application/json)
    
    + Body

            {
                "total": 1,
                "message": "Successful",
                "success": true,
                "data": null
            }
