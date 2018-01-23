**Better Chat** replaces the default chat in games by allowing you change and customize player name colors and prefixes. Plugins can add support for this plugin as well for compatibility, as running more than one chat plugin generally won't work otherwise.

**Note:** If you have this plugin installed and you may see somebody called **[Plugin Developer] LaserHydra**, that's me visiting your server.

***All arguments inside [ ] are optional! [time] should be a formatted time. Ex. 60m for 60 minutes. | stands for 'or'.***

## Commands

- **chat group add `<group>`** -- Creates a new chat group
- **chat group remove `<group>`** -- Removes a chat group
- **chat group set `<group> <setting> <value>`** -- Changes a chat group setting
- **chat group list** -- Lists all chat groups
- **chat user add `<player|steamid> <group>`** -- Adds a player to a chat group
- **chat user remove `<player|steamid> <group>`** -- Removes a player from a chat group
- **chat user groups `<player|steamid>`** -- List the chat groups of a player


## Permissions

This plugin uses Oxide's permission system. To assign a permission, use `oxide.grant user <name or steam id> <permission>`. To remove a permission, use `oxide.revoke user <name or steam id> <permission>`.

- **betterchat.admin** -- Required to use the the `chat` command

## Chat Formatting

You can do a lot with the formatting of a group. You can customize it with:

- **{Title}** = Group Title
- **{Username}** = Player Name
- **{ID}** = Player ID
- **{Message}** = Message
- **{Date}** = Date Stamp
- **{Time}** = Time Stamp
- **{Group}** = Primary Group

... but also just add words, letters, numbers, and symbols to it. You could just put the Title behind the name for example.

## Configuration

You can configure the settings in the `BetterChat.json` file under the `oxide/config` directory.

```json
{
    "Maximal Titles": 3
}
```

## Localization

The default messages are in the `BetterChat.json` file under the `oxide/lang/en` directory. To add support for another language, create a new language folder (ex. de for German) if not already created, copy the default language file to the new folder, and then customize the messages.

```json
{
  "Group Already Exists": "Group '{group}' already exists.",
  "Group Does Not Exist": "Group '{group}' doesn't exist.",
  "Group Field Changed": "Changed {field} to {value} for group '{group}'.",
  "Invalid Field": "{field} is not a valid field. Type 'chat group set' to list all existing fields.",
  "Invalid Value": "'{value}' is not a correct value for field '{field}'! Should be a '{type}'.",
  "Player Already In Group": "{player} already is in group '{group}'.",
  "Added To Group": "{player} was added to group '{group}'.",
  "Player Not In Group": "{player} is not in group '{group}'.",
  "Removed From Group": "{player} was removed from group '{group}'."
}
```

## For Developers

### Hooks

```csharp
OnBetterChat(Dictionary<string, object> data)
```

The data dictionary is entirely mutable - Change and return data dictionary to override chat message data
Dictionary<string, object>

- `Player (IPlayer)` - player sending the message
- `Text (string)` - text sent to chat
- `PrimaryGroup (string)` - name of players primary group
- `BlockedReceivers (List<string>)` - list of userids which should not receive the message
- `Username (Dictionary<string, object>)`
  - `Color (string)` - color of the username
  - `Size (int)` - font size of the username
- `Message (Dictionary<string, object>)`
  - `Color (string)` - color of the sent text
  - `Size (int)` - font size of the sent text
- `Format (Dictionary<string, object>)`
  - `Chat (string)` - format for chat output
  - `Console (string)` - format for console output

### API Calls

Easily edit your `oxide/data/BetterChat.json` file using the [BetterChat Group Manager](https://files.laserhydra.com/tools/groupmanager/Install%20BetterChat%20GroupManager.exe) _(Windows only)_.
