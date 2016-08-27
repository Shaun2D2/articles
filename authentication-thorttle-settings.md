## Customizing Laravel's Authentication Throttling

Laravel has a fantastic throttling system for general use with middleware, but did you know that you also have that advantage in your authentication controller out of the box? The framework will automatically lock out an IP address if attempting too many invalid login attempts. This is a great way to slow down attempted brute force attacks, but in some cases you may want to be more forgiving, or perhaps more strict when it comes to these default settings.  This article explores three different customization settings that you can easily add to your application if you need to modify its default behavior.

We will explore using Laravel 2.5's [ThrottlesLogins](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php) trait and mostly be working with the AuthController class located in app/Http/Controllers/Auth.

### Set Max Login Attempts
Lets say your feeling particularly forgiving today and want to allow your users 6 attempts to login before their IP get blocked.  You have the ability to set the maximum login attempts for a user simply by adding the following property to the top of AuthController class:
```
protected $maxLoginAttemps = 6; //max number of login attempts before throttle
```
You can set this to any integer you would like, by default [Laravel locks out after 5 attemps](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L120-L128).

### Set Lockout Time
Customizing the number of seconds the user's IP address is block is as simple as adding:
```
protected $lockoutTime = 60 //number of seconds
```
You are able to set this property to any number you wish and represents the number of seconds the user is locked out.  [Laravel sets this value to a default of 60 seconds](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L130-L138).

### Set throttle error message
Finally, another great thing you can customize is the error message that displays when a user is locked out.  Perhaps you don't want to show the number of seconds the user is unable to login.  You can simply edit the auth.php file located in /resources/lang/en.  This contains an array of messages that the [trait will use](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L70-L81).  Update the array value under 'throttle' and your message will now display accordingly.
```
'throttle' => 'Too many login attempts. Please try again later',
```

### Conclusion
We went over a few different ways you can customize Laravel's default authentication throttling behavior including max login attempts, lockout time, and error message.  Every application you build has its own needs so this may be very useful or you may want to keep the defaults.  Like many other things in the programming world, it just depends on the application your trying to build and what your needs are!
