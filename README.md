**Better Chat** replaces the default chat in games by allowing you change and customize player name colors and prefixes. Plugins can add support for this plugin as well for compatibility, as running more than one chat plugin generally won't work otherwise.

Easily edit your `oxide/data/BetterChat.json` file using the [BC Group Manager](https://files.laserhydra.com/tools/bcgroupmanager/setup.exe) *(Windows only)*.  

## Commands

All arguments inside **[ ]** are optional! **|** stands for 'or'.

- **chat group add `<group>`** -- Creates a new chat group
- **chat group remove `<group>`** -- Removes a chat group
- **chat group set `<group> <setting> <value>`** -- Changes a chat group setting
- **chat group list** -- Lists all chat groups
- **chat user add `<player|steamid> <group>`** -- Adds a player to a chat group
- **chat user remove `<player|steamid> <group>`** -- Removes a player from a chat group

## Permissions

- **betterchat.admin** -- Required to use the the `chat` command

## Frequently Asked Questions

**Question:** Why do all chat messages appear twice?  
**Answer::** You have another chat plugin installed, which isn't compatible with Better Chat. A usual suspect for this is `No Green`. Think about whether you really need that other plugin. No Green for example, can be easily recreated using Better Chat.  

**Question:** Why do clan tags not show?  
**Answer:** You might have to install the `Clan Tags` plugin to show them with Better Chat.  
  
**Question:** What do I need to set the 'priority' for?  
**Answer:** The priorities are used to determine the player's primary group and the order of titles displayed. For more information about the 'primary group', read "What does 'primary group' mean?" below.  
  
**Question:** I can't remove myself from the default/moderator/admin group  
**Answer:** Oxide automatically adds players to their appropriate groups. Everybody is added to the default group. If you are just trying to hide the default title for your admins, please look for the `HiddenIfNotPrimary` setting.  
  
**Question:** What does 'primary group' mean?  
**Answer:** The primary group is determined by the group's priorities. Out of all the groups the player is a part of, the one with the highest priority (the lowest number) is their primary group.  

## Configuration

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

## Chat Group Setup

For setting groups up, use the command 'chat'. If you want to set it up in the chat, you need to grant yourself the permission `betterchat.admin` and prefix the command with a forward slash (/). You can grant yourself the permission by typing the following command into the server console where you replace `<name or ID>` with your username or ID *(Steam ID for most games)*: `oxide.grant user <name or ID> betterchat.admin` Now you can use the command '/chat' in the chat.

First of all, create the group you want. Let's do that with the example of an admin group. *Remember*, if you are setting your groups up in the chat, you need to prefix the command with a forward slash (/).

To create a group, type: `chat group add admin`

You should also set the priority of the group, as it is very important for the plugin. The priority is the rank of the group and tells Better Chat which group should be prefered, if you are in multiple groups.

The lower the number, the higher the actual priority, meaning *0 > 1*. As admin is currently our highest priority group, set it to 0, if there is a moderator group too, it'd most likely be set it to 1 there: `chat group set admin priority 0`

Now as the group was created you can add yourself to it. Some games as for example Rust which have admins and moderator levels already, automatically apply you to the "admin" or "moderator" group if you have that admin or moderator level.

To manually add yourself to the group, use: `chat user add <name or ID> admin`

Now as you are in the group, you can give yourself a nice looking title: `chat group set admin title [Admin]`

You can also change the color of the title, for example to red: `chat group set admin titlecolor red`

It's a nice red [Admin] now. The colors can be any HEX color code or a common color spelling.

The same with your name: `chat group set admin namecolor red`

To finish it, you should change the priority of the default group which was automatically generated before, to 1 to be a lower priority than admin: `chat group set default priority 1`

There are many other group settings which can be set by using the `chat group set` command:

- **Priority** - rank of the group which tells the plugin which group to prefer if you are in multiple (the lower the number the higher the actual priority!)
- **TitleHiddenIfNotPrimary** - if set to true, the title of the group is hidden, if the group is not the one which the highest priority of the groups you are in
- **Title** - the groups title
- **TitleColor** - the color of the title
- **TitleSize** - the size of the title
- **TitleHidden** - if set to true, the title of the group will never be shown
- **UsernameColor** - the color of the username
- **UsernameSize** - the size of the username
- **MessageColor** - the color of the message
- **MessageSize** - the size of the message
- **ChatFormat** - the format/order of the chat message
- **ConsoleFormat** - the format/order of the chat message when displayed in console or logs

You can also change those values by editing the groups file: `oxide/data/BetterChat.json`.
Here, the same rules of editing apply as for the configuration file.

The default group file should look like this:

```json
[
  {
  "GroupName": "default",
  "Priority": 0,
  "Title": {
  "Text": "[Player]",
  "Color": "#55aaff",
  "Size": 15,
  "Hidden": false,
  "HiddenIfNotPrimary": false
  },
  "Username": {
  "Color": "#55aaff",
  "Size": 15
  },
  "Message": {
  "Color": "white",
  "Size": 15
  },
  "Format": {
  "Chat": "{Title} {Username}: {Message}",
  "Console": "{Title} {Username}: {Message}"
  }
  }
]
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
- `Username (string)` - username to be displayed in chat
- `Message (string)` - message sent to chat
- `ChatChannel (Chat.ChatChannel)` - IMMUTABLE & RUST ONLY : the channel the message is sent to
- `PrimaryGroup (string)` - name of players primary group
- `BlockedReceivers (List<string>)` - list of userids which should not receive the message
- `UsernameSettings (Dictionary<string, object>)`
  - `Color (string)` - color of the username
  - `Size (int)` - font size of the username
- `MessageSettings (Dictionary<string, object>)`
  - `Color (string)` - color of the sent text
  - `Size (int)` - font size of the sent text
- `FormatSettings (Dictionary<string, object>)`
  - `Chat (string)` - format for chat output
  - `Console (string)` - format for console output
- `CancelOption (int/ChatMessage.CancelOptions)`
  - `0` - don't cancel
  - `1` - cancel BetterChat handling only; default game chat won't be cancelled
  - `2` - cancel both BetterChat handling & default game chat

### API Calls

To create a new chat group:
```csharp
private bool API_AddGroup(string group)
```

To get existing chat groups:
```csharp
private List<JObject> API_GetAllGroups(IPlayer player)
```

To get chat groups a player is in:
```csharp
private List<JObject> API_GetUserGroups(IPlayer player)
```

To register a title for players:
```csharp
private void API_RegisterThirdPartyTitle(Plugin plugin, Func<IPlayer, string> titleGetter)
```

To get the formatted message for a player:
```csharp
private string API_GetFormattedMessage(IPlayer player, string message, bool console = false)
```

To get the formatted username for a player:
```csharp
private string API_GetFormattedUsername(IPlayer player)
```

To set a field on a chat group:
```csharp
private ChatGroup.SetFieldResult? API_SetGroupField(string group, string field, string value)
```

To check if a chat group exists:
```csharp
private bool API_GroupExists(string group)
```