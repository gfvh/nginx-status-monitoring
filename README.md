nginx-zabbix-template for 3.x version
=====================

Description
-----------
This is Zabbix monitoring solution to monitor nginx web servers status directly from Zabbix server as external script. At nginx node is needed only to enable nginx_status

Bourne shell script nginx_status.sh gives following options

Monitoring information:

* active
* accepts
* handled
* requests
* reading
* writing
* waiting

NGINX Config
------------

Add these lines to inside server {..} block and after that reload nginx

```
  location /nginx_status/ {
        # Turn on nginx stats
        stub_status on;
        # I do not need logs for stats
        access_log   off;
        # Security: Only allow access from IP #
        # Define acl IP in here
        allow ZABBIX_SERVER_IP_TO_ADD;
        # Deny rest #
        deny all;
    }

```

Installation in the Zabbix Server
---------------------------------

Look for the external scripts directory in your Zabbix Server configuration file. 
CentOS RPM Zabbix installing: 

``` 
 /usr/lib/zabbix/externalscripts 
```

Copy the bourne shell script there. chmod +x 

Import template Template_Nginx_Status_Info_Zabbix.xml

Define macros {$HOST_PORT} for different port number and {$HOST_CONN} for adding nginx ip. PS! Underline, not dots
