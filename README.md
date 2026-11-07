# Spotify for MyGo Music

English | [简体中文](README.zh-CN.md)

Browse and control Spotify from [MyGo Music](https://github.com/egoist/mygo-music). It isn't affiliated with or endorsed by Spotify.

The sound comes from a Spotify Connect device: Spotify's own app on this computer or your phone, a speaker, or anything else your account plays on. MyGo Music shows your library and tells that device what to play. With [librespot](https://github.com/librespot-org/librespot) installed, this computer is such a device without Spotify's app open.

**Playing needs Spotify Premium.**

## Set up

1. Sign in to the [Spotify developer dashboard](https://developer.spotify.com/dashboard) with a Premium account and click **Create app**. Give it any name and description, add this redirect URI, tick **Web API**, agree to the terms and save:

   ```
   http://127.0.0.1:43110/callback
   ```

   Type it exactly: `localhost`, or a slash at the end, doesn't match.
2. Install the plugin with the deeplink:

   [mygo-music://install-plugin?repo=xingkaixin/mygo-music-spotify](mygo-music://install-plugin?repo=xingkaixin/mygo-music-spotify)

   Or paste the GitHub URL in Settings > Plugins:

   [https://github.com/xingkaixin/mygo-music-spotify](https://github.com/xingkaixin/mygo-music-spotify)
3. Copy the **Client ID** from the app's page in the dashboard. In MyGo Music, paste it in the plugin's settings, click **Sign In** and approve access in your browser.
4. Open Spotify on a device, or set up librespot as below, then play something in MyGo Music. Choose another device from the player's device menu.

Only the account that made the app, and the accounts added to it, can sign in. Spotify's Development Mode lets in five at most. To add one, open the app in the dashboard, go to **User Management**, and enter the account's name and email.

## Playing without Spotify's app

1. Install librespot with Homebrew. The plugin looks for it in Homebrew's folders, `/opt/homebrew/bin` and `/usr/local/bin`.

   ```
   brew install librespot
   ```
2. In MyGo Music, open Settings > Plugins > Spotify and allow it to start programs.
3. Play something. The first time, your browser opens a Spotify page to sign librespot in. It's a sign-in of its own, apart from the plugin's: approve it with the same account. If the song hasn't started by then, play it again.

librespot plays on this computer at 320 kbps, as the device **MyGo Music**. It's used when no other device is playing and you haven't chosen another in the device menu. It starts with the first song you play and stops when MyGo Music quits.

To sign librespot in with another account, quit MyGo Music, delete `~/Library/Application Support/MyGo Music/plugin-data/spotify/librespot`, and play again.

For some accounts, newer ones especially, Spotify refuses librespot the keys to the songs, and it plays nothing ([librespot#1649](https://github.com/librespot-org/librespot/issues/1649)). Then play through Spotify's app.

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

## When something goes wrong

**Invalid redirect URI**, on Spotify's page when you sign in: the app in the dashboard doesn't have `http://127.0.0.1:43110/callback` exactly. Add it, save, and sign in again.

**Spotify won't let this account in: add it under User Management in your app's dashboard, and check the app's owner has Premium**, right after you sign in: Spotify's Development Mode lets in only the account that made the app and the accounts added under **User Management**, and only while the account that made the app has Premium. If your browser was signed in to Spotify with another account, sign out of it there first. Fix whichever applies, then sign in again.

**Open Spotify on this computer, your phone or a speaker, then play again**: no Spotify device is online. Open Spotify's app on one, or set up librespot. Right after librespot's first sign-in, play again.

**Playing through Spotify needs Premium**: the account you signed in with is on Spotify Free.

**Spotify is limiting requests: try again in a moment**: Spotify limits how often an app in Development Mode asks, and how much in all. It counts for your developer account, so making another app doesn't help. Wait, then try again.

**Nothing loads, where Spotify needs a proxy**: MyGo Music and librespot connect to Spotify directly and don't use the system proxy setting. Turn on your proxy's TUN mode, sometimes called enhanced mode.

## Privacy

Your Spotify tokens are kept unencrypted in the plugin's data on this machine and are sent only to Spotify. Signing out forgets them; librespot's sign-in stays in the plugin's data, in the `librespot` folder, until you delete it. To revoke access on Spotify's side, remove the app on your Spotify account's **Manage apps** page.

Each song's title, artist, album and length go to LRCLIB to find its lyrics.
