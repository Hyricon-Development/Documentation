---
sidebar_position: 3
---

# Configuration
This page goes over the `settings.json` configuration and setting up the Nginx webserver for Faliactyl.

## Configuring your Settings
Because the `settings.json` file is so large, this page will break down and explain each individual section.

```json
{
  "version": "1.4.1",
  "defaulttheme": "tinydash",
  "website": {
    "port": 8080,
    "secret": ""
  }
```

The start of the settings file; The `port` is where Faliactyl will be running on reverse proxy.

```json
  "guildblacklist": {
    "guilds": ["ServerID", "ServerID"]
  },
```

This section allows you to blacklist guild's and stop users form using your hosting 

```json
  "pterodactyl": {
    "domain": "Pterodactyl URL",
    "key": "Pterodactyl API Key"
  },
```

This section focuses on the panel side of configuration. domain is your Pterodactyl domain. This must be prefixed with https:// to work. If you are hosting locally then localhost:<PORT> can be used (with additional paths if applicable). key is the Pterodactyl Application API key for Faliactyl. This can be found or created by going to your.pterodactyl.domain/admin/api. This must be kept secret at all times as it can be used to expose confidential information and destroy your panel.

```json
  "limits": {
    "ram": 1024,
    "cpu": 200,
    "servers": 4,
    "disk": 5120
  },
```
This allows you to control the maximum amount of resources anyone can buy from the resources store.

```json
   "ads": {
     "top": {
       "enabled": false,
    },
     "bottom": {
       "enabled": false,
    }
  },
```

This allows you to add ads in your dashbaord 
`ads`  Paste your Adsense/Adsterra script in /themes/YourFaliactylTheme/components/ads.ejs
`ads2` Paste your Adsense/Adsterra script in /themes/YourFaliactylTheme/components/ads2.ejs

```json
  "status": {
    "enabled": false,
    "url": "",
   },
```
This allows you to add your status page in the dashbaord
You need a HetrixTools status page setup for this to work. You can create one at [Hetrixtools](https://hetrixtools.com) works with uptime robot to
Go to [Hetrixtools Dashboard Status Page](https://hetrixtools.com/dashboard/status-pages/) click the settings icon under actions and click Embed Report then copy and paste your HetrixTools page script into /themes/YourFaliactylTheme/components/status.ejs. this works with uptime robot to.

```json
       "bot": {
         "token": "bot token",
         "joinguild": {
           "enabled": false,
           "guildid": ["SERVERID", "SERVERID"],
           "forcejoin": false,
           "registeredrole": null
}
```

This section is where you need to add your bot token of bot which allow users to join the server when the login to dashbaord


```json
      "webhook": {
        "webhook_url": "",
        "auditlogs": {
          "enabled": true,
          "disabled": []
        }
      },
```

This section is for configuring audit logs in Faliactyl. 
`enabled` will determine if you want to activate this system or not, to activate it you must leave it in `true`, to deactivate it in `false`. `webhook_url` is the URL of your webhook, in this case you must put the URL of the webhook created on your Discord server.

```json
      "passwordgenerator": {
        "signup": true,
        "note": "Use this to disable signups",
        "length": 8
      },
```

This allow users to regen there password if they forget it. You can set the length of the password 

```json
      "oauth2": {
        "id": "discord oauth2 application id",
        "secret": "discord oauth2 application secret",
        "link": "discord oauth2 application link without the '/callback'",
        "callbackpath": "/callback",
        "prompt": true,
        "ip": {
          "trust x-forwarded-for": true,
          "block": [],
          "duplicate check": false
        }
      },
```

Your Discord credentials can be found [at the developer portal](https://discord.com/developers/applications) with the application you are using for Faliactyl. When setting up the `callbackpath`, make sure it is also whitelisted in the portal: __Your Application > Oauth2 > Redirects__. The `token` is the token of your bot application for Faliactyl. This must be kept secret __at all times__ as it can be easily abused. The `guild` is your server ID if applicable. This is optional and is used to add clients to your server when logging into the dashboard.

```json
      "packages": {
        "default": "default",
        "list": {
          "default": {
            "ram": 1024,
            "disk": 1024,
            "cpu": 100,
            "servers": 1
          }
        }
      },
```
The packages displayed when a user is creating a server through Faliactyl. These packages can be customised and used with Faliactyl's currency system. The options shown are the specifications for the server(s) that will be given to the user in that package.

```json
      "locations": {
        "1": {
          "name": "Example Location 1",
          "package": null
        },
        "2": {
          "name": "Example Location 2",
          "package": null
        }
      },
```

This section is for the location used for creating the servers on Pterodactyl.

`"1"` is the location ID, you can find it on your Pterodactyl Panel, inside the admin area. `Locations -> Search your location, and you should see the ID on the left.`
`name` is the location name that you want to show while creating a server on Faliactyl.
`enabled` is pretty self-explanatory. It means if the location is enabled or not inside Faliactyl.
`package` checks if a user has a package on his account. If the user doesn't have the specified package in Faliactyl, the user won't be able to create the server in that location. 

```json
      "eggs": {
       "paper": {
          "display": "Minecraft Java",
          "minimum": {
            "ram": 1024,
            "disk": 1024,
            "cpu": 100
          },
          "maximum": {
            "ram": null,
            "disk": null,
            "cpu": null
          },
          "info": {
            "egg": 3,
            "docker_image": "ghcr.io/pterodactyl/yolks:java_17",
            "startup": "java -Xms128M -Xmx{{SERVER_MEMORY}}M -Dterminal.jline=false -Dterminal.ansi=true -jar {{SERVER_JARFILE}}",
            "environment": {
              "SERVER_JARFILE": "server.jar",
              "BUILD_NUMBER": "latest"
            },
            "feature_limits": {
              "databases": 4,
              "backups": 4
            }
          }
        },
        "bungeecord": {
          "display": "Minecraft BungeeCord",
          "minimum": {
            "ram": 512,
            "disk": 512,
            "cpu": 75
          },
          "maximum": {
            "ram": null,
            "disk": null,
            "cpu": null
          },
          "info": {
            "egg": 1,
            "docker_image": "ghcr.io/pterodactyl/yolks:java_17",
            "startup": "java -Xms128M -Xmx{{SERVER_MEMORY}}M -jar {{SERVER_JARFILE}}",
            "environment": {
              "SERVER_JARFILE": "bungeecord.jar",
              "BUNGEE_VERSION": "latest"
            },
            "feature_limits": {
              "databases": 4,
              "backups": 4
            }
          }
        }
      },
```

This section is for the server configuration eggs in Pterodactyl. When creating a server through Faliactyl, the package associated with this egg will be used to create it. You can set this to your liking, and/or remove the default egg to change it with another one.

```json
      "coins": {
        "enabled": true,
        "store": {
          "_comment": "The cost and per is not intended to used with 0. This is not intended to sell resources for coins. Make sure coins are enabled too, or else there can be errors.",
          "enabled": true,
          "ram": {
            "cost": 100,
            "per": 1
          },
          "disk": {
            "cost": 100,
            "per": 1
          },
          "cpu": {
            "cost": 100,
            "per": 1
          },
          "servers": {
            "cost": 100,
            "per": 1
          },
          "databases": {
            "cost": 100,
            "per": 1
          },
          "allocations": {
            "cost": 100,
            "per": 1
          },
          "backups": {
            "cost": 100,
            "per": 1  
          }
        }
      }
    },
```

This section is for the Faliactyl store configuration. `enabled` is whether the item should be purchasable in the shop. `cost` is how much the item costs and `per` is the amount of that item to give per purchase.

```json
    "minero": {
      "_comment": "You can get a public key on https://minero.cc. You can get money using minero.cc.",
      "enabled": false,
      "key": "Minero Public Key"
    },
```

This Section Mining users Computer/Laptop this will mine user's cpu when they are afk on afk page

```json
    "arcio": {	
      "enabled": false,	
      "widgetid": "Arc Widget ID",	
      "afk page": {	
        "enabled": true,	
        "path": "afkwspath",	
        "every": 60,	
        "coins": 1
      }	
    }
  }
}
```

Afk And [Arc](https://arc.io) this allow users to afk and gain coin's 

