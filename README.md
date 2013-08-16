# Installation

Make sure you have successfully bootstrapped a Juju Environment. We're going to set up a small environment for Zabbix to monitor.

    juju deploy mysql
    juju deploy mediawiki
    juju add-relation mysql mediawiki:db
    juju expose mediawiki

Next, deploy the zabbix charm and zabbix-agent subordinate

    juju deploy zabbix
    juju deploy zabbix-agent

If you haven't already, deploy MySQL

    juju deploy mysql

Then add the relation from MySQL to Zabbix server

    juju add-relation mysql zabbix

Create a relation between zabbix and zabbix-agent. This establies the agent <-> remote-agent relationship

    juju add-relation zabbix zabbix-agent

Finally, attach the subordinate to the services you with to monitor in your environment

    juju add-relation zabbix-agent mysql
    juju add-relation zabbix-agent mediawiki

These services should automatically show up in Zabbix after the subordinate it setup.

# Configuration

In order for auto-discovery to work, you must add the autodiscovery action to the configuration of Zabbix webpanel:
https://www.zabbix.com/wiki/howto/config/autoregister

# Caveats

# Help

File bugs, ask questions, author email
