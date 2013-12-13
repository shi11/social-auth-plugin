social-auth-plugin
=======================

Cordova (PhoneGap) 3.0+ Plugin to authenticate with Facebook/Twitter accounts on iOS 

Notes:
* Prerequisite: A Cordova 3.0+ project for iOS 6+
* This is designed to only work with accounts tied to the OS (set up in Settings).  This does not include fallbacks to use a web-based auth if no accounts are found. 

#Installing

This plugin follows the Cordova 3.0 plugin spec, so it can be installed through the Cordova CLI in your existing Cordova project:
```bash
cordova plugin add https://github.com/danwilson/social-auth-plugin.git
```
If you are not using the CLI, follow the steps in the section [Installing Without the CLI](#nocli)

Once installed, you will need to modify SocialAuthPlugin.m to add your App ID for Facebook and your Consumer Key and Consumer Secret for Twitter:
`
#define TW_CONSUMER_KEY              @""
#define TW_CONSUMER_SECRET           @""
#define FB_APP_ID                    @""
`
This will likely change in the future... once I determine a better way to avoid having to modify the Objective C files.

#JavaScript Usage
(After 'deviceready' has been called)

Login to Facebook:
* `window.socialAuth.loginFacebook(function success() {}, function error() {})` 
If permission is granted, returns access token and basic profile info. If not granted, it returns "Error"

Check if one or more Twitter accounts are available (this is the entry point for the Twitter flow):
* `window.socialAuth.isTwitterAvailable(function success() {}, function error() {})` 
If permission is granted, returns account. If not granted, it returns "Error"

Get all available Twitter usernames:
* `window.socialAuth.returnTwitterAccounts(function success() {}, function error() {})`
On success, returns an array of strings.

Perform Reverse Auth (to get OAuth tokens needed for logins):
* `window.socialAuth.performTwitterReverseAuthentication(function success() {}, function error() {})` 
On success, returns a string with necessary tokens (in OAUth form, like a query string)


#Installing Without the CLI <a name="nocli"></a>
Copy the files manually into your project and add the following to your config.xml files:
```xml  
<feature name="SocialAuth">  
  <param name="ios-package" value="SocialAuthPlugin" />  
</feature> 
```
