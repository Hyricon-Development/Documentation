---
sidebar_position: 3
---

# Configuration
This page goes over the `settings.yml` configuration and setting up the Nginx webserver for Faliactyl.

## Configuring your Settings
Because the `settings.yml` file is so large, this page will break down and explain each individual section.

```yml
name: Faliactyl
defaulttheme: default
version: 2.0.0
website:
  port: 8080
  secret: Example Secret
```
The start of the settings file; The `port` is where Faliactyl will be running on reverse proxy.

```yml
gift:
  enabled: true
```
This allow you to gift resources form your account to your friends account `Ram` `Disk` `CPU` `Coins` 

```yml
discordserver:
  enabled: true
  invitelink: https://discord.gg/yourcode
```
This allow users to join your discord server 
[image](https://cdn.discordapp.com/attachments/994261490427248790/997176112482369627/unknown.png)

```yml
ads:
  enabled: false
  script: ''
```
This allow you to add ads in your dashbaord/client panel/area 

```yml
guildblacklist:
  guilds:
  - ServerID
  - ServerID
```
This `Backlist` users to use your dashboard who are there in a guild

```yml
pterodactyl:
  domain: ""
  key: ""
```
This section focuses on the panel side of configuration. `domain` is your Pterodactyl domain. This must be prefixed with `https://` to work. If you are hosting locally then `localhost:<PORT>` can be used (with additional paths if applicable). `key` is the Pterodactyl Application API key for Faliactyl. This can be found or created by going to `your.pterodactyl.domain/admin/api`. This must be kept secret at all times as it can be used to expose confidential information and destroy your panel. `generate_password_on_sign_up` is whether to create a new password for new accounts or use a default password.

```yml
linkvertise:
  enabled: true
  userid: 000000
  coins: 20
```
This section allow users to gain coins by clicking link and ads


```yml
status:
  enabled: true
  script: ""
```
This allows you to add your status page in the dashbaord
You need a HetrixTools status page setup for this to work. You can create one at [Hetrixtools](https://hetrixtools.com) works with uptime robot to
Go to [Hetrixtools Dashboard Status Page](https://hetrixtools.com/dashboard/status-pages/) click the settings icon under actions and click Embed Report then copy and paste your HetrixTools page script into /themes/YourFaliactylTheme/components/status.ejs. this works with uptime robot to.

```yml
stripe:
  enabled: true  
  key: 0000000000 # Replace this with your Stripe API Key
  coins: 200 # Coins per amount in USD
  amount: 1 # usd
```

This allow users to buy coins form `STRIPE` ! 

```yml
smtp:
  enabled: false
  host: Example Host
  port: 7080
  username: Example Username
  password: Example Password
```
This section is for the configuration of the email system, better known as SMTP in Faliactyl. For this to work you will need to have an SMTP host like Mailjet/MailCow. `enabled` will determine if you want to activate this system or not, to activate it you must leave it in `true`, to deactivate it in `false`. `host` will determine the host you are using, example: smtp.zoho.com or smtp.gmail.com `port` will determine the port your host uses, in some cases it can be `25`, `465`, etc. `usernamer` is the user provided by your SMTP host, in some cases it can be your email. `password`

```yml
api:
  client:
    j4r: 
      enabled: true
      ads:
      - name: Example Server 1
        id: 
        invite: https://discord.gg/yourcode
        coins: 50
      - name: Example Server 2
        id: 
        invite: https://discord.gg/yourcode
        coins: 50
```
This allow users to join a server an gain coins

```yml
    Role Packages:
      enabled: false
      Server: SERVERID # Replace SERVERID with your Guild/Server ID
      list: # Replace ROLEID with the Role ID, you can add as many as you want.
        RoleID: Package Name 
```
This allow users to get role in discord and dashboard
Replace `SERVERID` with your Discord Server ID

```yml
    bot:
      token: ""
      joinguild:
        enabled: false
        guildid:
        - SERVERID
        - SERVERID
        forcejoin: false
        registeredrole: ""
```

This section allow users to join your discord server `Force` when they login to the dash

```yml
    webhook:
      webhook_url: ''
      auditlogs:
        enabled: false
        disabled: []

```

This section allow you to see the logs like who login to dash, who buy server, modify server, and more

```yml
    passwordgenerator:
      signup: true 
      length: 8
```

This Section allow users to get there panel login password and they can reset it also 
make `signup` to false to disable login

```yml
    oauth2:
      id: ""
      secret: ""
      link: ""
      callbackpath: "/callback"
      prompt: true
```

This section is made for login go to [Discord Dev Portal](https://discord.dev) create a bot 
`id` add the bot id, `secret` add the bot secret, `link` add the link of your dashboard

```yml
    packages:
      default: default
      list:
        default:
          ram: 1024
          disk: 1024
          cpu: 100
          servers: 1
          databases: 2
          allocations: 2
          backups: 2
```
This is section is where you can set users default resources 

```yml
    locations:
      '1':
        name: Example Location 1
        package: null
      '2':
        name: Example Location 2
        package: null
```
This Section allow you to add your location/nodes into the dashboard 

```yml
    eggs:
      paper:
        display: Minecraft Java
        minimum:
          ram: 1024
          disk: 1024
          cpu: 100
        maximum:
          ram: 2000
          disk: 2000
          cpu: 2000
        info:
          egg: 3
          docker_image: ghcr.io/pterodactyl/yolks:java_17
          startup: java -Xms128M -Xmx{{SERVER_MEMORY}}M -Dterminal.jline=false -Dterminal.ansi=true
            -jar {{SERVER_JARFILE}}
          environment:
            SERVER_JARFILE: server.jar
            BUILD_NUMBER: latest
          feature_limits:
            databases: 4
            backups: 4
```

This Section allow you to add the details of the egg 

```yml
    coins:
      enabled: true
      store:
        enabled: true
        ram:
          cost: 100
          per: 1
        disk:
          cost: 100
          per: 1
        cpu:
          cost: 100
          per: 1
        servers:
          cost: 100
          per: 1
        databases:
          cost: 100
          per: 1
        ports:
          cost: 100
          per: 1
        backups:
          cost: 100
          per: 1
```

This section is for the Faliactyl store configuration. `enabled` is whether the item should be purchasable in the shop. `cost` is how much the item costs and `per` is the amount of that item to give per purchase.
 
```yml
  minero:
    enabled: false
    key: Minero Public Key
```

This mine users pc while they are on the dashboard page

```yml
  arcio:
    enabled: false
    widgetid: Arc Widget ID
    afk page:
      enabled: true
      path: afkwspath
      every: 60
      coins: 1
```

This is used for earing money by afking users

```yml
widget:
  enabled: false
  server_id: GUILD_ID
  channel_Id: CHANNEL_ID
```

This allow users to ask support form dashboard to discord form the dash page
