---
title: "Music Assistant Setup Guide (December 2025)"
sidebar_position: 2
---

# Connecting View Assist to Music Assistant

This guide provides up-to-date, step-by-step instructions for connecting View Assist to Music Assistant using the latest versions available as of December 2025.

## System Requirements

- **Home Assistant OS**: Version 2025.12.x or later
- **Music Assistant**: Version 2.7 or later (released December 2025)
- **View Assist Integration**: Latest version from HACS
- A working View Assist satellite device (Android tablet, ESPHome device, etc.)

## What's New in Music Assistant 2.7

Music Assistant 2.7 (December 2025) includes significant improvements:

- **Redesigned UI**: Sleeker navigation with improved onboarding
- **Built-in Player**: Preview music directly in your browser
- **User Profiles**: Create tailored profiles for each family member with individual music providers and device access
- **Secure Authentication**: Profile-based authentication with Home Assistant SSO support
- **Multi-room Sync**: SensPin protocol for perfectly synchronized multi-room playback
- **Smart Crossfade**: Beat and BPM-analyzed transitions between tracks
- **Remote Access**: WebRTC streaming allows music playback from anywhere with internet access
- **Enhanced Metadata**: Improved support for lyrics, cover art, and track details
- **Expanded Integrations**: Supports Apple Music, Spotify, YouTube Music, Tidal, SiriusXM, SoundCloud, Plex, Jellyfin, BBC Sounds, and more

## Step 1: Install Music Assistant

1. Navigate to **Settings > Add-ons** in Home Assistant
2. Open the **Add-on Store**
3. Search for "**Music Assistant**"
4. Click **Install**
5. After installation completes:
   - Enable "**Start on Boot**" for reliability
   - Enable "**Watchdog**" to automatically restart if it crashes
6. Click **Start** to launch the add-on
7. Check the **Logs** tab for any startup errors

## Step 2: Configure Music Assistant

### Access the Music Assistant Interface

1. Click "**Open Web UI**" from the Music Assistant add-on page
2. The Music Assistant interface will open in a new tab
3. Follow the initial setup wizard

### Add Music Sources

You can combine multiple music sources:

**Streaming Services:**
- Spotify
- Apple Music
- YouTube Music
- Tidal
- SiriusXM
- SoundCloud
- Others

**Local Sources:**
- Local music folders on your Home Assistant server
- Network shares (NAS devices)
- Plex or Jellyfin servers

**To add a music source:**
1. In Music Assistant, go to **Settings > Music Providers**
2. Click **+ Add Provider**
3. Select your desired service
4. Follow the authentication steps
5. Allow time for initial library synchronization (this may take several minutes to hours depending on library size)

:::warning Offline Playback Limitations
Music Assistant 2.7 does **not** support offline playback for streaming services like Spotify. Streaming providers require an active internet connection and work via their respective protocols (e.g., Spotify Connect). 

**For offline playback:**
- Use local music files stored on your Home Assistant server or NAS
- Local files can be played without an internet connection
- Spotify playlists cannot be cached locally for offline use due to API and DRM restrictions

This is a known limitation, and offline caching for streaming services is a feature under consideration for future releases.
:::

## Step 3: Discover and Configure Audio Players

Music Assistant will auto-discover compatible media players on your network:

**Supported Player Types:**
- Google Cast
- Sonos
- AirPlay / AirPlay 2
- DLNA / UPnP
- HomePods
- Chromecast
- And many more

**To configure players:**
1. In Music Assistant, go to **Settings > Players**
2. Review the discovered players
3. Enable/disable players as needed
4. Configure player groups for multi-room audio if desired

:::note
Amazon Echo (Alexa) devices have limited support due to Amazon API restrictions
:::

## Step 4: Set Up User Profiles (Optional but Recommended)

Music Assistant 2.7 introduces user profiles for personalized experiences:

1. Go to **Settings > User Profiles**
2. Click **+ Create Profile**
3. Configure each profile:
   - Link to specific music providers
   - Set content restrictions
   - Assign speaker/device access
   - Enable Home Assistant SSO for easier management

This is particularly useful for families with multiple users and different music preferences.

## Step 5: Install View Assist Integration

If you haven't already installed View Assist:

### Install via HACS

1. Ensure HACS is installed in your Home Assistant instance
   - If not, visit [HACS installation guide](https://hacs.xyz/docs/setup/download)
2. In Home Assistant, go to **HACS**
3. Click the three dots menu > **Custom repositories**
4. Add the repository: `https://github.com/dinki/view_assist_integration/`
5. Category: **Integration**
6. Click **Add**
7. Find **View Assist** in HACS and click **Download**
8. **Restart Home Assistant**

### Configure View Assist Integration

1. Go to **Settings > Devices & Services**
2. Click **+ Add Integration**
3. Search for "**View Assist**"
4. Follow the setup wizard to add your View Assist devices

## Step 6: Connect View Assist to Music Assistant

### Configure the Music Player Device

For each View Assist satellite that you want to use with Music Assistant:

1. Go to **Settings > Devices & Services > View Assist**
2. Click on your View Assist device
3. Find the **musicplayer_device** configuration option
4. Select a Music Assistant player device from the dropdown
   - This should be a Music Assistant player entity
   - Typically named the same as your `mediaplayer_device` but with a `_2` suffix
   - Example: If your media player is `media_player.living_room`, the Music Assistant player might be `media_player.living_room_2`

:::tip
Music Assistant creates its own media player entities that are separate from your original Home Assistant media players. Look for the Music Assistant-created players in your entity list.
:::

### Verify the Connection

1. Open Music Assistant web interface
2. Select a Music Assistant player that corresponds to your View Assist device
3. Try playing some music
4. Verify that:
   - Music plays on the correct device
   - The Music view appears on your View Assist display (if configured)
   - Playback controls work properly

## Step 7: Install Music Blueprints for Voice Control

To control Music Assistant via voice commands on your View Assist devices:

### Install the Music View

The Music view is automatically installed via the View Assist integration. No additional steps needed.

### Install Music Control Blueprints

1. **Play Music with Music Assistant**: [Blueprint documentation](./sentences/play-music-with-ma.md)
   - Allows voice commands like: "Play some Beatles music"
   - "Play the artist Taylor Swift"
   - "Play the song Bohemian Rhapsody by Queen"

2. **Play Radio with Music Assistant**: [Blueprint documentation](./sentences/play-radio-with-ma.md)
   - Allows voice commands for TuneIn and Radio Browser stations
   - Example: "Play KEXP radio"

### Import Blueprints

1. Go to **Settings > Automations & Scenes > Blueprints**
2. Click **Import Blueprint**
3. Copy the blueprint URLs from the documentation pages above
4. Configure each blueprint according to your devices and preferences

## Step 8: Test Your Setup

### Test Voice Commands

Try these voice commands on your View Assist device:

- "Play some jazz music"
- "Play the artist Miles Davis"
- "Play the song Blue in Green by Miles Davis"
- "Queue Coltrane"
- "What's playing?"
- "Skip this song"
- "Pause music"
- "Resume music"

### Test Multi-room Audio (Optional)

If you have multiple speakers:

1. Create a player group in Music Assistant
2. Use voice commands to play music on the group
3. Verify synchronization across all speakers

### Test Remote Access (Optional)

If you enabled WebRTC streaming:

1. Access your Home Assistant instance from outside your network
2. Open Music Assistant
3. Try playing music remotely
4. Verify that streaming works properly

## Troubleshooting

### Music Assistant Player Not Showing in View Assist

- Restart both the Music Assistant add-on and Home Assistant
- Check that Music Assistant has fully initialized (check add-on logs)
- Verify your media players are discovered in Music Assistant
- Look for Music Assistant entities in **Developer Tools > States** (filter by "media_player")

### Music Not Playing

- Check that your music providers are properly authenticated
- Verify library synchronization is complete
- Test playback directly in Music Assistant UI
- Check the Music Assistant logs for errors

### Voice Commands Not Working

- Verify the blueprints are properly configured
- Check that the `musicplayer_device` is correctly set in View Assist device configuration
- Test the Assist pipeline separately to ensure voice recognition works
- Review automation traces in Home Assistant to debug failed commands

### Synchronization Issues in Multi-room Setup

- Use speakers from the same manufacturer/protocol for best sync
- Check network quality - ensure all speakers have good WiFi/Ethernet connection
- Try the SensPin protocol if supported by your speakers
- Some combinations of different speaker types may have inherent sync limitations

## Advanced Features

### Smart Crossfade

Enable in Music Assistant settings for seamless transitions:
1. Go to **Settings > Playback**
2. Enable **Smart Crossfade**
3. Adjust fade duration and BPM-matching settings

### Lyrics and Metadata

Music Assistant 2.7 includes enhanced metadata support:
- Lyrics display (when available)
- Rich cover art
- Extended track information
- Artist biographies (from connected providers)

### Automations and Scripts

Integrate Music Assistant with Home Assistant automations:

```yaml
# Example: Play music when arriving home
automation:
  - alias: "Welcome Home Music"
    trigger:
      - platform: state
        entity_id: person.your_name
        to: "home"
    action:
      - service: media_player.play_media
        target:
          entity_id: media_player.living_room_2  # Your Music Assistant player
        data:
          media_content_id: "library://playlists/welcome-home"
          media_content_type: "playlist"
```

## Additional Resources

- [Official Music Assistant Documentation](https://music-assistant.io/)
- [Music Assistant GitHub Repository](https://github.com/music-assistant/server)
- [Home Assistant Community Forums](https://community.home-assistant.io/)
- [View Assist Discord Community](https://discord.gg/viewassist) (if available)
- [Music Assistant 2.7 Release Blog Post](https://www.home-assistant.io/blog/2025/12/17/music-assistant-2-7/)

## Version Notes

This guide is current as of **December 2025** and reflects:
- Home Assistant OS 2025.12.x
- Music Assistant version 2.7
- Latest View Assist integration releases

Music Assistant and View Assist are actively developed projects. Check the official documentation for the most current information and new features.

## Getting Help

If you encounter issues:

1. Check the troubleshooting section above
2. Review the Music Assistant logs in the add-on interface
3. Check View Assist integration logs in Home Assistant
4. Search the Home Assistant community forums
5. Ask for help in the View Assist or Music Assistant community channels

Remember to include:
- Your Home Assistant version
- Music Assistant version
- Error messages from logs
- Steps to reproduce the issue
