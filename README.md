**Better Chat** replaces the default chat in games by allowing you change and customize player name colors and prefixes. Plugins can add support for this plugin as well for compatibility, as running more than one chat plugin generally won't work otherwise.

Easily edit your `oxide/data/BetterChat.json` file using the [BetterChat Group Manager](https://files.laserhydra.com/tools/groupmanager/Install%20BetterChat%20GroupManager.exe) *(Windows only)*.

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

You can configure the settings in the `BetterChat.json` file under the `oxide/config` directory. It's recommended to use a JSON editor for editing the config file or validation site such as jsonlint.com to prevent syntax errors.

The file should look like this (in a code/text editor):

```json
{
  "Maximal Characters Per Message": 128,
  "Maximal Titles": 3
}
```

Every setting looks like this: `"Key": Value`

The key is the name/description of the setting while the value is the actual value you want to set it to. For example, to enable the word filter, you see under/inside `"Word Filter" { ... }` there is `"Enabled": false`. To enable it, you change it to `"Enabled": true`.

- **Maximal Titles** -- The maximum amount of titles to display
- **Maximal Characters Per Message** -- The maximum characters per message to display

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

## Frequently Asked Questions

**Question:** Why do clan tags not show? \
**Answer:** Please install the Clan Tags plugin to show them with Better Chat.

**Question:** I can't remove myself from the default/moderator/admin group \
**Answer:** Oxide automatically adds players to their appropriate groups. Everybody is added to the default group. If you are just trying to hide the default title for your admins, please look for the `HiddenIfNotPrimary` setting.


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

```csharp
private bool API_AddGroup(string group)
```

```csharp
private List<object> API_GetUserGroups(IPlayer player)
```

```csharp
private void API_RegisterThirdPartyTitle(Plugin plugin, Func<IPlayer, string> titleGetter)
```

```csharp
private string API_GetFormattedMessage(IPlayer player, string message, bool console = false)
```

```csharp
private string API_GetFormattedUsername(IPlayer player)
```

```csharp
private ChatGroup.SetFieldResult? API_SetGroupField(string group, string field, string value)
```

```csharp
private bool API_GroupExists(string group)
```
