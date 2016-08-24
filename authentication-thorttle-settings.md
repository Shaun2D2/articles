## Laravel Authentication Throttle Settings

Laravel has a fantastic throttling system for general use with middleware, but did you know that you also have that advantage in your authentication controller out of the box?  Laravel provides a very simple way to manage these settings, but it is not immediately obvious from the documentation that you can alter the default settings directy in your AuthController.

There are two particular useful settings we will dive into.  Just as a side note, we are using Laravel 2.5's [ThrottlesLogins](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php) trait and you will need to use the AuthController in app/Http/Auth/Controller.php.

### Setting Max Login Attempts
You have the ability to set the maximum login attemps for a user simply by adding:
```
protected $maxLoginAttemps = 5 //number of login attemps
```
to the top of your AuthController controller.  You can set this to any integer you would like, by default [Laravel locks out after 5 attemps](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L120-L128).

### Set Lockout Time
You can also opt to change the number of seconds you wish to lock a user out.  You can do this by adding:
```
protected $lockoutTime = 60 //number of seconds 
```
You can set this property to any number you wish and represents the number of seconds the user is locked out.  So if you wish to lock a user out for 1 hour, then you'd update this value to 3600.  [Laravel sets this vaule to a default of 60 seconds](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L130-L138).

### use your own thorttle message
Finally, another great thing you can customize is the error.  Prehaps you don't wnat to show the number of seconds the user is lockedo out.  You can simply edit the auth.php file located in resources/lang/en.  This contains an array of messages that the [trait will use](https://github.com/laravel/framework/blob/5.2/src/Illuminate/Foundation/Auth/ThrottlesLogins.php#L70-L81).  Simply update the array value under 'throttle' and your message will now display accordingly.
```
'throttle' => 'Too many login attempts. Please try again later',
```

### Conclusion
We went over a few different ways you can update your authetentication thorottling including max login attempts and lockout time.  Every application you build has it's own needs so this may be very useful or you may want to keep the defaults, they are indeed sensable!  Thanks for reading and look forward to you seeing more.
