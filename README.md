ownCloud log file decoder and rules for OSSEC (Open Source SECurity)
==============

One of the main features of OSSEC is monitoring system and application logs. This repository covers the decoder and rules for a ownCloud service.

# HowTo Use #

To add the `owncloud.log` file to the configuration for monitoring is simple. In the system’s `/var/ossec/etc/ossec.conf` on your server add an entry like this:

```xml
<ossec_config>

  <!-- .... -->

  <localfile>
    <log_format>syslog</log_format>
    <location>/var/www/PATH_TO_YOUR_OWNCLOUD_INSTALL/data/owncloud.log</location>
  </localfile>
</ossec_config>
```

Now add the compiler from `ossec/etc/local_decoder.xml` to your `/var/ossec/etc/local_decoder.xml` file on your server. If it doesn't exist, create it. This one will parse your `owncloud.log` so you can apply the rules.

Now copy the rules from `ossec/rules/owncloud_rules.xml` to `/var/ossec/rules/owncloud_rules.xml` on your server.

Last thing is to load these newly added rules. Open the system’s `/var/ossec/etc/ossec.conf` on your server again and add an entry like this:

```xml
<ossec_config>
  
  <!-- .... -->
  
  </rules>
  
    <!-- .... -->
  
    <include>owncloud_rules.xml</include>
  </rules>
</ossec_config>
```

Only thing left is to reload your ossec:

`$ sudo /var/ossec/bin/ossec-control restart`
