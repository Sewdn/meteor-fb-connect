#meteor-fb-connect

## Facebook Connect package to connect facebook users to existing users.

### Why use this package?

#### use case 1
Your users might have registered to your app using the email/password based registration process. When they decide to connect their facebook account, they are (without this package) currently being forced to logout, create a new account using fb-login. At this point you might have added custom logic on a onCreatUser callback to look for duplicate users...

No more... If you want to connect allready authenticated users in your app to their fb-account, this package provides extra methods in the Meteor's Account package to do this the proper way. Add a facebook connect button inside their profile, and add their fb profile to their meteor-app-profile. The next time they login, they can use the (unmodified) facebook-login button.

#### use case 2
You don't use facebook login. You have millions of users that have properly registered to your service, using their email and providing a password for authentication. Now you decide to add facebook login functionality nevertheless. Your loggedin users notice the facebook connect-button in their profile (from use case 1) and make the connection.

But there are millions of other users who will notice, the next time they want to login, that fancy facebook login button. Without this package, they end up with 2 accounts.

No more... When they use the facebook-login button, their existing account is searched for based on the email-address facebook returns. If this email was found, the facebook profile is addeded and the next time they login, they can use the (unmodified) facebook-login button.

### How to use
Just install the package:
```bash
$ mrt install facebook-connect
```

You get email-based existing user detection out of the box for facebook-login. No onCreateUser callback will run, because no new user will be created of the user was found.

When you want to add a facebook-connect button in your user's profile pages, just add an event handler:

```javascript
Template.facebookConnect.events({
  'click span.connectFacebook' : function () {
    Meteor.connectWithFacebook(options, function () {
      console.log(arguments);
    });
  }
});
```

Meteor.connectWithFacebook is completely analogue to the Meteor.loginWithFacebook method from the account-facebook package (http://docs.meteor.com/#meteor_loginwithexternalservice)