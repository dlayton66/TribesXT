# Tribes XT Installation Instructions

Latest release: 01/02/2024

1. Download the plugin: [Tribes XT](https://github.com/dlayton66/TribesXT/raw/main/TribesXT.dll)
2. Put plugin in `C:\Tribes\plugins`
3. Add the following variables to `C:\Tribes\config\autoexec.cs` or a separate `*.acs.cs` file
  ```
  // Offset for inserting server snapshots into the client interpolation buffer
  $net::timeNudge = 48;
  // How far to allow the client's synced clock to drift from the server before correcting
  $net::clientClockCorrection = 8;

  // Customize the size of chaingun tracer bullets
  $pref::tracerWidth = 1.0;
  $pref::tracerLength = 1.0;

  // Center third person camera above head like 1.40
  $pref::newThirdPerson = false;

  // Change damage flash opacity (only on XT servers)
  $pref::damageFlash = 0.35;
  ```
4. Customize the variables
   * `$net::timeNudge`
     * For XT servers, use the default value of 48.
     * For vanilla servers, set to `32 - ping`.  For instance, a player who pings 64 should use `$net::timeNudge = -32`.
5. Connect to a Tribes XT server
    * `Tribes XT - Mod Required discord.gg/za2wgkvv`
    * `connect("216.128.150.208:28088");`

## What is Tribes XT?
Tribes XT is a plugin developed by Altimor for [Starsiege: Tribes](https://en.wikipedia.org/wiki/Starsiege:_Tribes) which aims to modernize its netcode and minimize player input lag.

By default, a Tribes server waits for input from the client and simply responds to that input when it's received.  If a player pinging 250ms attempts to fire a disc, that disc will be fired on the server at least 250ms after the input was given, and the client will not see that disc has been fired locally until it receives a response from the server.  This leads to an experience with significant input lag that is heavily dependent on a player's connection.

In Tribes XT, that disc is fired immediately on the client, reducing input lag to be almost nonexistent.  When the server receives notice that the disc was fired, it retroactively adjusts to account for when that occurred on the client, syncing up what a player sees on their client and what happens on the server.  The cumulative effect of this is an extremely smooth and responsive experience regardless of a player's connection.

## Current features
- Instant mouse input response
- Serverside aim/movement lag fixes
- Lag compensation
- Subtick shooting
- New terp code
- Improved packet send timing
- Better chaingun tracer rendering

## FAQ

### Does TribesXT work on every server?
Yes!  The impact is very noticeable even on vanilla servers.  However, XT was designed to be run on XT servers, so for the best experience a player should connect to a Tribes XT server.

### What is a vanilla server?
A server that is not running Tribes XT.

### What do I do with netset.dll?
Tribes XT completely replaces PredictForwardTime and Interpolate.  Netset.dll can be completely removed.
