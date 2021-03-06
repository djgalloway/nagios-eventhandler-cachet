# nagios-eventhandler-cachet
A Nagios event handler to push Nagios notifications to Cachet API

## Prerequisites
 - Have a working Cachet installation
 - Have created some Cachet components to play with
 - Have a Nagios instance with PHP CLI and php-curl installed

## Installation

 - Get a Cachet API key: Create a new user in Cachet dashboard, login with this user, and get the API key in his profile.
 - Clone this repo to /usr/share/nagios3/plugins/eventhandlers (depending on your configuration)
 - Rename config.inc.php.example to config.inc.php and replace the Cachet credentials with your own
 - Try it: `./cachet_notify 'My Cachet component' 'My nagios service' CRITICAL HARD 'The service is Critical'`

## Configuration

 - Make a Nagios command:
```
  define command {
      command_name    cachet_notify
      command_line    /usr/share/nagios3/plugins/eventhandlers/cachet_notify '$ARG1$' '$SERVICEDESC$ - $HOSTADDRESS$' '$SERVICESTATE$' '$SERVICESTATETYPE$' '$SERVICEOUTPUT$' '$LONGSERVICEOUTPUT$'
  }
```
 - Add an event handler on your services:
```
  define service {
      service_description             My nagios service
      ...
      event_handler                   cachet_notify!My Cachet component
  }
```
 - Restart nagios

