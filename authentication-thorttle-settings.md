## Customizing Laravel's Authentication Throttling

Laravel has a fantastic throttling system for general use with middleware, but did you know that you also have that advantage in your authentication controller out of the box? The framework automatically locks out an IP address if too many invalid login attempts are detected, this could slow down someone attempting to gain unauthorized access to an account. However, in some cases, you may want to be more forgiving, or stricter when it comes to the defaults.

Following are three different customization settings that you can easily add to your application if you need to modify its behavior. We will learn how to override Laravel 2.5's [ThrottlesLogins](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php) trait by working mostly with the AuthController class located in app/Http/Controllers/Auth.

### Set Max Login Attempts
Laravel [locks an IP address out](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L120-L128) after 5 invalid login attempts.  This could be an undesired default for your application so you have the ability to set the maximum login attempts simply by adding the following property to the top of AuthController class:
```
protected $maxLoginAttemps = 6; //max number of login attempts before throttle
```
Now each IP address will have a maimum of 6 allowed attempts before they are throttled.  Of course, this can be changed to any number you see fit.

### Set Lockout Time
It's possible to customize the number of seconds a user is blocked. To do this, add:
```
protected $lockoutTime = 60 //number of seconds
```
Set this property to number of seconds the user should be locked out of the application.  [Laravel sets this value to a default of 60 seconds](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L130-L138).

### Set throttle error message
You also have the ability to customize the error message that is returned when a user is locked out. If you don't want the default error message to display to the user,  you can simply edit the auth.php file located in /resources/lang/en. This file contains an array of preset messages that you can configure. Update the array value under 'throttle' and the new message will display.
```
'throttle' => 'Too many login attempts. Please try again later',
```

Now you know how to customize Laravel's default authentication throttling behavior, including max login attempts, lockout time, and error message. Every application you build has its own needs, so this may be very useful or you may want to keep the defaults. Like many other things in the programming world, it just depends on the application your trying to build and what your needs are.
