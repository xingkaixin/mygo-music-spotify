# Spotify for MyGo Music

Browse and control Spotify from [MyGo Music](https://github.com/egoist/mygo-music). It isn't affiliated with or endorsed by Spotify.

The sound comes from a Spotify Connect device: Spotify's own app on this computer or your phone, a speaker, or anything else your account plays on. MyGo Music shows your library and tells that device what to play. With [librespot](https://github.com/librespot-org/librespot) installed, this computer is such a device without Spotify's app open.

**Playing needs Spotify Premium.**

## Set up

1. In the [Spotify developer dashboard](https://developer.spotify.com/dashboard), click **Create app**. Tick **Web API**, and add this redirect URI exactly:

   ```
   http://127.0.0.1:43110/callback
   ```

   Spotify asks for Premium on the account that creates the app.
2. Install the plugin with the deeplink:

   [mygo-music://install-plugin?repo=xingkaixin/mygo-music-spotify](mygo-music://install-plugin?repo=xingkaixin/mygo-music-spotify)

   Or paste the GitHub URL in Settings > Plugins:

   [https://github.com/xingkaixin/mygo-music-spotify](https://github.com/xingkaixin/mygo-music-spotify)
3. In the plugin's settings, paste the app's **Client ID**, then click **Sign In** and approve access in your browser.
4. Open Spotify on a device, or set up librespot as below, then play something in MyGo Music. Choose another device from the player's device menu.

An app in Spotify's Development Mode lets in five accounts at most. To share yours, add the other accounts under **User Management** in the dashboard.

## Playing without Spotify's app

1. Install librespot:

   ```
   brew install librespot
   ```
2. In MyGo Music, open Settings > Plugins > Spotify and allow it to start programs.
3. Play something. The first time, your browser opens a Spotify page to sign librespot in: approve it with the same account, then play again if nothing started.

librespot plays on this computer as the device **MyGo Music**. It's used when no other device is playing and you haven't chosen one. It runs while MyGo Music does.

## The MyGo Music Queue playlist

Spotify's desktop app doesn't play a list of songs sent to it, only a playlist or an album. So the first time you play, the plugin makes a private playlist named **MyGo Music Queue** in your library, and each time you play it writes what's up next there, up to 100 songs, and plays it. MyGo Music hides it from its sidebar; Spotify's apps show it. Don't edit it: it's rewritten each time. If you delete it, the plugin makes a new one the next time you play.

## What works

- Home, made of your recently played songs, top tracks, top artists and saved albums
- Search for songs, albums, artists, playlists and podcasts
- Albums, artists, your playlists, liked songs, saved albums and podcasts
- Liking songs, saving albums, playlists and podcasts
- Creating, renaming and deleting playlists, and adding, removing and reordering their songs
- Play, pause, seek, volume and choosing a device
- Timed lyrics from [LRCLIB](https://lrclib.net), when it has them

## What Spotify doesn't let it do

Spotify's Web API gives apps in Development Mode less than its own apps have:

- Playlists you don't own or collaborate on, Spotify's own included, show in the sidebar but can't be opened.
- There are no editorial shelves, charts, new releases, recommendations or radio.
- An artist's top tracks aren't available. The artist page shows what a search for their name ranks first.
- Following artists isn't available.
- Search returns 10 results a page.

## Privacy

Your Spotify tokens are kept unencrypted in the plugin's data on this machine and are sent only to Spotify. Signing out forgets them; librespot's sign-in stays in the plugin's data, in the `librespot` folder, until you delete it. To revoke access on Spotify's side, remove the app on your Spotify account's **Manage apps** page.

Each song's title, artist, album and length go to LRCLIB to find its lyrics.
