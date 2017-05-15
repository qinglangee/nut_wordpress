# nginx proxy_cache_valid   作用时间

>> 1. proxy_cache_valid is set to 1h and upstream's response is valid for 2h.
>
> nginx will cache for 2h.
>
>> 2. proxy_cache_valid is set to 2h and upstream's response is valid for 1h.
>
> nginx will cache for 1h.
>
>> 3. proxy_cache_valid is set to 1h and upstream's response doesn't
>> contain any caching hints.
>
> nginx will cache for 1h.

This just means that upstream's caching instructions are more important than proxy_cache_valid, right?

*Yes. 也就是说tomcat的caching指令比nginx的proxy_cache_valie参数更重要*



refs:
http://forum.nginx.org/read.php?2,6298,6298#REPLY  
http://forum.nginx.org/read.php?2,2182,2184#msg-2184  


[1]: http://forum.nginx.org/read.php?2,6298,6298#REPLY
