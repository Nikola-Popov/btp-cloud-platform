<!-- loio9d24198eed554793b7eb279657f17971 -->

# sessionTimeout

Define the amount of time \(in minutes\) for which a session can remain inactive before it closes automatically \(times out\); the default time out is 15 minutes.



> ### Note:  
> We recommend using the environment variable [SESSION\_TIMEOUT](environment-variables-ba52705.md#loioba527058dc4d423a9e0a69ecc67f4593__section_blz_hgn_mv) to configure the session timeout.
> 
> If the environment variable [SESSION\_TIMEOUT](environment-variables-ba52705.md#loioba527058dc4d423a9e0a69ecc67f4593__section_blz_hgn_mv) is set this property will be overwritten.

> ### Sample Code:  
> ```
> {
>   "sessionTimeout": 40
> }
> ```

With the configuration in the example above, a session timeout will be triggered after 40 minutes and involves central log out.

A session timeout triggers a central log out with the following consequences:

-   Deletes the user session
-   Requests the log out paths for all your back-end services \(if you provided these paths in the `destinations` and `service` properties\).

> ### Note:  
> `sessionTimeout` can only be configured in the central routing configuration file \(xs-app.json\) that belongs to the application router, not in an xs-app.json file that is part of an HTML5 application.

