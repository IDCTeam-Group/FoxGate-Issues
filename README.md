<center>

[![Join the discord server.](https://cdn.modrinth.com/data/cached_images/b00caabc5d76ec659ca50db9f17f0866de5f1b83.png)](http://discord.idcteam.xyz/)</center>

**FoxGate** `(formerly, FoxAntiVPN)` is a **powerful tool designed to protect your Minecraft server from unwanted visitors using VPNs.** This plugin prevents players from bypass ip bans by allowing server owners to detect and block **VPN's**, **Proxy's** and **more**. This plugin connects to a configerable list of services which detect VPN's without any hassel. **This plugin is extremely hard to bypass.** With numerous APIs working together, **bypassing this AntiVPN is very difficult**. The more services you enable, the harder it becomes for users to evade detection. Currently supporting **BungeeCord** `+ Forks`, **Velocity** `+ Forks` and **FOLIA**.
<br />
<br />
### Features:
- Supports different types of databases: **H2**, **SQLite**, **PostgreSQL**, **MySQL** and **MariaDB** with **HikariCP** connection.
  
<details>
<summary>Reference: Configuration of database.</summary>

```
#      ___      _        _
#     /   \__ _| |_ __ _| |__   __ _ ___  ___
#    / /\ / _` | __/ _` | '_ \ / _` / __|/ _ \
#   / /_// (_| | || (_| | |_) | (_| \__ \  __/
#  /___,' \__,_|\__\__,_|_.__/ \__,_|___/\___|

# Configure a database for use.
database:

    # - Available options in type.
    #   All options use HikariCP for better performance.
    #  |=> MySQL
    #  |=> MariaDB
    #  |=> PostgreSQL
    #  |=> SQLite
    #  |=> H2
    #
    # If you change this configuration and your server is already
    # started. You can use the command "/foxgate db reconnect" to
    # apply the changes without restarting plugin or server.
    # Remember first reload the plugin with "/foxgate reload"
    # and use that command.
    type: "sqlite"
    # Edit table in case you want a different.
    # If you want to use your actually stats (of 1.0.5-pre4 or older),
    # use the next:
    # - "vpn_cache"
    table: "foxgate"
   
    # MariaDB/MySQL databases type. Edit here.
    remote:
     # Determine information of your database.
      hostname: "localhost"
      port: 3306
      database: "foxav_db"
      username: "root"
      password: "password123"
     
      # These settings apply to the MySQL/MariaDB connection pool (HikariCP).
      # - Default values are suitable for most users. Only modify these if you know what you're doing!
      pool-settings:

        # The maximum number of connections in the connection pool.
        # - Determines the upper limit of active database connections that can be managed simultaneously.
        # - Setting this too high can overload your database server, while setting it too low can cause delays.
        # Example:
        #   If your server has high traffic and the database can handle it, set this to 10 or higher.
        # Recommended: 4
        # More information: https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing
        maximum-pool-size: 4

        # Minimum number of idle connections to maintain in the pool.
        # - The pool will try to maintain this number of idle (inactive) connections ready for use.
        # - Setting this equal to 'maximum-pool-size' creates a fixed-size connection pool,
        #   ensuring consistent resource allocation.
        # Example:
        #   For a server with occasional traffic spikes, set this to half of 'maximum-pool-size'.
        # Recommended: 4
        minimum-idle: 4

        # Maximum lifetime of a connection in the pool, in milliseconds.
        # - Connections older than this value will be closed and replaced.
        # - This prevents stale connections from lingering indefinitely and reduces database timeout issues.
        # - Should be at least 30 seconds less than the timeout imposed by the database itself.
        # Example:
        #   If your database timeout is 30 minutes, set this value to 25 minutes (1500000 ms).
        # Recommended: 1500000 (25 minutes)
        maximum-lifetime: 1500000

        # Frequency of pings to keep the connection alive, in milliseconds.
        # - This prevents connections from being closed due to inactivity (common in many databases or firewalls).
        # - Must be less than 'maximum-lifetime' and greater than 30 seconds (30000 ms).
        # Example:
        #   For long-running servers, a value of 10 minutes (600000 ms) is generally ideal.
        # Recommended: 600000 (10 minutes)
        keepalive-time: 600000

        # The maximum time in milliseconds to wait for a connection from the pool.
        # - If no connection is available within this time, an exception will be thrown.
        # - Setting a low value ensures responsiveness but may cause issues under heavy load.
        # Example:
        #   For responsive applications, a value between 3-5 seconds (3000-5000 ms) is ideal.
        # Recommended: 5000 (5 seconds)
        connection-timeout: 5000

        # Custom validation timeout (time taken to validate a connection), in milliseconds.
        # - Determines how long the pool will wait while testing if a connection is still valid.
        # - A low value improves responsiveness, but setting it too low may cause false negatives.
        # Example:
        #   For most databases, 3 seconds (3000 ms) is sufficient for validation.
        # Recommended: 3000 (3 seconds)
        validation-timeout: 3000
 
      # Custom properties for advanced users.
      # Add any additional properties to fine-tune the connection.
      #
      # You can uncomment unnecesary properties or remove,
      # also edit to values that is perfect for you.
      # (!) THIS PROPERTIES IS BASED WITH SUPPORT
      # MARIADB, IF YOU GET ERROR IN MYSQL, YOU CAN
      # ADAPT OR CONSIDERING TO CHANGE TO MARIADB,
      # THAT WORKS WITH MYSQL DATABASES.
      properties:

        # - SSL.
        # Database connection settings.
        # Adjust these properties to optimize the connection with your MySQL/MariaDB server.
        # Enables or disables SSL for secure connections.
        # It is highly recommended to set this to true if your server supports SSL.
        # Default is false, as many MySQL/MariaDB servers do not support SSL.
        sslMode: "disabled"
        requireSSL: "false"                   # If set to "true", forces SSL connections. Overrides 'sslMode'.
        verifyServerCertificate: "false"      # Validates the server's SSL certificate. Set to "true" for production.
        # - Connection Optimization
        cachePrepStmts: "true"                # Enables prepared statement caching
        prepStmtCacheSize: "250"              # Number of prepared statements to cache
        prepStmtCacheSqlLimit: "2048"         # Maximum size of a query in the cache
        useServerPrepStmts: "true"            # Uses server-side prepared statements
        # - Performance and Buffering
        rewriteBatchedStatements: "true"      # Optimizes batch insert/update performance
        useCompression: "false"               # Enables compression for data transfer (optional)
        maintainTimeStats: "false"            # Disables time statistics for improved performance
        autoReconnect: "true"                 # Automatically reconnects if the connection is lost
        # - Character Encoding
        # Specifies whether Unicode character encoding should be used.
        # If working with multilingual data, this is highly recommended.
        useUnicode: "true"
        # Defines the character encoding for the database connection.
        # Use "utf8" for compatibility with most character sets.
        characterEncoding: "utf8"
        # - Time Zone
        serverTimezone: "UTC"                 # Ensures consistent timezone handling

    postgresql:
      hostname: "localhost"
      port: 5432
      database: "foxav_db"
      username: "postgres"
      password: "password123"

      # Database connection settings for PostgreSQL.
      settings:

        # Adjust these properties to optimize the connection with your PostgreSQL server.
        # Enables or disables SSL for secure connections.
        # It is highly recommended to set this to true if your server supports SSL.
        # Default is false.
        ssl: false
        # The maximum time in seconds to wait for a connection from the pool.
        # Choose a value between 1 and 5 for a balance between availability and performance.
        # Recommended: 3.0
        connectiontimeout: 3.0

        # Specifies whether Unicode character encoding should be used.
        # PostgreSQL natively supports Unicode, so this can be left as true.
        useUnicode: true

        # Defines the character encoding for the database connection.
        # Use "UTF-8" to handle multilingual data and ensure compatibility.
        characterEncoding: "UTF-8"

        # Keeps idle connections alive.
        tcpKeepAlive: true

        # Timeout for socket operations in seconds.
        socketTimeout: 30

        # Number of prepared statement executions before switching to server-side prepared statements.
        prepareThreshold: 5

        # Application name for debugging or monitoring purposes.
        applicationName: "FoxGate"

        # Enables optimized binary transfer for certain data types.
        binaryTransfer: true
     
      # These settings apply to this PostgreSQL, because uses Hikari for connection.
      # - Default values are suitable for most users. Only modify these if you know what you're doing!
      pool-settings:

        # The maximum number of connections in the connection pool.
        # - Determines the upper limit of active database connections that can be managed simultaneously.
        # - Setting this too high can overload your database server, while setting it too low can cause delays.
        # Example:
        #   If your server has high traffic and the database can handle it, set this to 10 or higher.
        # Recommended: 10
        # More information: https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing
        maximum-pool-size: 10

        # Minimum number of idle connections to maintain in the pool.
        # - The pool will try to maintain this number of idle (inactive) connections ready for use.
        # - Setting this equal to 'maximum-pool-size' creates a fixed-size connection pool,
        #   ensuring consistent resource allocation.
        # Example:
        #   For a server with occasional traffic spikes, set this to half of 'maximum-pool-size'.
        # Recommended: 2
        minimum-idle: 2

        # Sets the maximum time an idle connection can remain in the pool before being automatically closed.
        # - Connections that remain idle for longer than the configured value will be removed from the pool
        #   and replaced with new connections as needed.
        # - This is useful to free up resources and keep connections "fresh" avoiding possible problems with
        #   stale connections.
        # Recommended: 600000 (10 minutes)
        idle-timeout: 600000

        # Maximum lifetime of a connection in the pool, in milliseconds.
        # - Connections older than this value will be closed and replaced.
        # - This prevents stale connections from lingering indefinitely and reduces database timeout issues.
        # - Should be at least 30 seconds less than the timeout imposed by the database itself.
        # Example:
        #   If your database timeout is 30 minutes, set this value to 25 minutes (1500000 ms).
        # Recommended: 1800000 (30 minutes)
        maximum-lifetime: 1800000

        # The maximum time in milliseconds to wait for a connection from the pool.
        # - If no connection is available within this time, an exception will be thrown.
        # - Setting a low value ensures responsiveness but may cause issues under heavy load.
        # Example:
        #   For responsive applications, a value between 30-50 seconds (30000-50000 ms) is ideal.
        # Recommended: 30000 (30 seconds)
        connection-timeout: 30000

    sqlite:
      file: "FoxGate.db"
   
      # These settings apply to this SQLite, because uses Hikari for connection.
      # - Default values are suitable for most users. Only modify these if you know what you're doing!
      #
      # Yeah... I know HikariCP isn't better to use with SQLite, but is only for avoid any
      # type of errors! Please, don't kill me!
      pool-settings:

        # The maximum number of connections in the connection pool.
        # - Determines the upper limit of active database connections that can be managed simultaneously.
        # - Setting this too high can overload your database server, while setting it too low can cause delays.
        # Example:
        #   If your server has high traffic and the database can handle it, set this to 10 or higher.
        # Recommended: 5
        # More information: https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing
        maximum-pool-size: 5

        # Minimum number of idle connections to maintain in the pool.
        # - The pool will try to maintain this number of idle (inactive) connections ready for use.
        # - Setting this equal to 'maximum-pool-size' creates a fixed-size connection pool,
        #   ensuring consistent resource allocation.
        # Example:
        #   For a server with occasional traffic spikes, set this to half of 'maximum-pool-size'.
        # Recommended: 1
        minimum-idle: 1

        # Maximum lifetime of a connection in the pool, in milliseconds.
        # - Connections older than this value will be closed and replaced.
        # - This prevents stale connections from lingering indefinitely and reduces database timeout issues.
        # - Should be at least 30 seconds less than the timeout imposed by the database itself.
        # Example:
        #   If your database timeout is 30 minutes, set this value to 25 minutes (1500000 ms).
        # Recommended: 1800000 (30 minutes)
        maximum-lifetime: 1800000

        # The maximum time in milliseconds to wait for a connection from the pool.
        # - If no connection is available within this time, an exception will be thrown.
        # - Setting a low value ensures responsiveness but may cause issues under heavy load.
        # Example:
        #   For responsive applications, a value between 30-50 seconds (30000-50000 ms) is ideal.
        # Recommended: 30000 (30 seconds)
        connection-timeout: 30000

    h2:
      file: "h2db"

    # When an IP isn't detected a vpn or proxy, this need to save in
    # cache to don't make more requests for a little time for save
    # performance and requests, customizable here.
    bypass:
       # Enable this feature?
        enable: true

        # Determine the amount in hours to save the IP in cache and avoid
        # make more requests to this IP. Useful to save performance and
        # verify only one time for certain time.
        #
        # Recommended: 2
        expiration_time: 2

    # When an IP is detected in a result, this is save in the cache
    # to don't make more request for a little time, this value is
    # saved in hours.
    #
    # Recommended: 36
    expiration_time: 36
```
</details>

- This plugin has minimal performance impact due to it running **asynchronously**.
- Customize the messages how you want! This plugins supports **MiniMessage** and **Legacy** colors in all versions.
- The default config is setup to block most VPN's, although you can **[add a custom service](https://www.spigotmc.org/resources/116596/field?field=documentation)** or **modify existing services in the config**.
- This plugin will automatically download lists of VPN's from services that don't have an API.


### Services available in the default config.
> **Do the services in the config works correctly?**
> The list of services in the default config have all been tested at least once. You can still configure each services values as well as edit or add more services (like in the example above). Services may not always function due to issues on their end or because of how they where added to the config. 

Some services are **disabled by default** because **they require an API key to function**. However, **ten of these services** work without a key and are enabled by default, providing basic **VPN** and **proxy** detection right away. To maximize protection against **VPNs**, **proxies**, and **other threats**, it is recommended to obtain API keys for the remaining services. Doing so will enhance the accuracy and effectiveness of detection.

✅is a free service, no key required for work.
<br />
⭕is a paid/key required service, key required for work.
<br />
<br />
✅ **IP-API**
<br />
✅ **BlackBox**
<br />
✅ **Rayzsde** `(knowed: ProVPN)`
<br />
✅ **SkyDB**
<br />
✅ **FunkeMunky** `(knowed: Kauri)`
<br />
✅ **IP2Location**
<br />
✅ **IPRisk**
<br />
✅ **IPdb-Amelia** `(knowed: YAAntiVPN)`
<br />
✅ **FreeIPAPI**
<br />
✅ **Negativity**
<br />
⭕ **BanProxy**
<br />
⭕ **GetIPIntel**
<br />
⭕ **VPN-API.xyz**
<br />
⭕ **VPNBlocker**
<br />
⭕ **IPQualityScore**
<br />
⭕ **IDCTeam** `(our, discord support)`
<br />
⭕ **ProxyCheck**
<br />
⭕ **VPNAPI**
<br />
⭕ **AntiVPN.net**
<br />
⭕ **AntiVPN.io**
<br />
⭕ **IPHub**
<br />
⭕ **IPHunter**
<br />
<br />
**Want to know how to configure these services?** Check the configuration section below for examples and templates. When a player is detected using a **VPN** or **proxy**, the plugin automatically stores this information in a **database**. This prevents repeated **API requests** for the same **IP address** for a configurable number of hours, **reducing unnecessary API calls** and **improving efficiency**.

By using both services that are enabled-by-default and those that require API keys, you can create a robust detection system that effectively identifies and blocks **VPN**, **proxy**, and **other undesired connections**. See more information in the [**documentation section**](https://www.spigotmc.org/resources/116596/field?field=documentation).
<br />
<br />
### Commands.
- **/foxgate <add/remove> <IP> [allow/deny]:** Add or remove an IP from the database, this is used to restrict or allow access by an IP.
- **/foxgate verbose:** Enable/Disable verbose output.
- **/foxgate reload:** Reload the config files.
- **/foxgate db <purge/reconnect>:** Reconnect to the database or purge information from it.
- **/foxgate status <ip>:** View information about an IP registered in the database.

### Permissions.
- **foxav.notifications** - Get notified when a user is detected with **VPN**.
- **foxav.command** - Access all **FoxGate** commands.
- **foxav.bypass** -  Bypass detection by **FoxGate**.
<br />

- [SpigotMC](https://www.spigotmc.org/resources/116596/)
- [Modrinth](https://modrinth.com/plugin/foxgate)
- [Hangar](https://hangar.papermc.io/NovaCraft254/FoxGate)
- [Polymart](https://polymart.org/resource/6563)
- [BuiltByBit](https://builtbybit.com/resources/51990/)
- [CurseForge](https://www.curseforge.com/minecraft/bukkit-plugins/foxgate)
