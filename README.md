# homebridge-people-textfile
This is a plugin for homebridge. It monitors who is at home, based on searching for names in a textfile.
It is based on the excellent plugin "homebridge-people" from PeteLawrence.

# Installation

1. Install homebridge (if not already installed) using: npm install -g homebridge
2. Install this plugin using: npm install -g homebridge-people
3. Update your configuration file. See below for a sample.

# Configuration

```
"accessories": [
	{
    "accessory" : "people",
    "name" : "People",
    "people" : [
      { "name" : "Pete", "target" : "Pete Miller" },
      { "name" : "Me", "target" : "John Doe" }
    ],
    "threshold" : 15
  }
],
```

# How it works
* When started homebridge-people will continually search a textfile with each person defined in config.json.
* When a ping is successful the current timestamp is logged to a file (seen.db.json)
* When a Homekit enabled app looks up the state of a person, the last seen time for that persons device is compared to the current time minus ```threshold``` seconds, and if it is greater assumes that the person is active.

# Notes
## Running on a raspberry pi as non 'pi' user
On some versions of raspbian, users are not able to use the ping program by default.  If none of your devices show online try running ```sudo chmod u+s /bin/ping```.  Thanks to oberstmueller for the tip.
