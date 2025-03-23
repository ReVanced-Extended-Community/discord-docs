# Webhooks
Webhooks are used for official messages (such as in ⁠`#📌・links`) so that they can be edited by any Admin. [discohook.org](https://discohook.org/) is a good tool to initialize and edit webhook messages. (It's easiest to all use this since all of the messages use a single default color.)

### Editing an existing webhook message
To edit a webhook message, open the settings of the channel the message is in and go to Integrations > Webhooks. Select the webhook to edit and copy the webhook URL. Go to the message in the channel and copy the message link. Go to [discohook.org](https://discohook.org/)  and press the `Clear All` button near the top. Paste the webhook URL in the textbox near the top, and paste the message link near the bottom. Press the `Load` button beside the message link textbox. The embed contents will load, and you can edit it. When you are done, press the `Edit` button beside the webhook URL textbox.

### Creating a new webhook message
To create a webhook message, open the settings for the channel the message should be sent in and go to Integrations > Webhooks. You can either create a new webhook or use an existing one in that channel if the name encompasses what your webhook message will do.

When creating a webhook, clearly name it and upload the image below as its avatar.

<img src="/assets/red_rvx_logo.png" width="400"/>

Once you have the webhook you will use, copy the webhook URL. Go to [discohook.org](https://discohook.org/)  and press the `Clear All` button near the top. Paste the webhook URL in the textbox near the top. Open the `Profile` dropdown, and enter "ReVanced Extended" as the username. (This can't be changed later. If no username is given, the name of the webhook will be its displayed name.)

Create the message you want to send. Generally, embeds are best, except when the character limit must exceed 2000 characters. For consistency, follow the same formatting as other webhook embeds in the server. When you are done, press the `Send` button beside the webhook URL textbox.

### Formatting Roles, users, etc.
https://discord.com/developers/docs/reference#message-formatting 



# Role selection
Role reactions are used instead of Discord's onboarding feature because onboarding requires the `@everyone` role to have the `Send messages` permission in 5 channels. To accomplish this, we would need to add another channel, such as a meme or bot channel, which clutter the server and make moderation more difficult.

The role reactions are handled by YAGPDB. It is initially configured on the dashboard at https://yagpdb.xyz/manage/1270729807948415048/rolecommands/ and then implemented with the `/rolemenu create` command in the channel where you want the role reaction menu to be. Refer to YouTube tutorials or the YAGPDB documentation for more info.



# Autorole
YAGPDB gives the `@Member` role to all members after they agree to the server rules prompt. The autorole function is configured at https://yagpdb.xyz/manage/1270729807948415048/autorole 



# Custom YAGPDB commands
Custom commands through YAGPDB are used to streamline the troubleshooting and support processes by giving users and helpers the ability to quickly retrieve commonly used information and links.

### Creating custom commands
Custom commands are set up at https://yagpdb.xyz/manage/1270729807948415048/customcommands/. Commands are sorted into groups, which share designated settings. Commands related to support should ofc be in the Support group. For other functions, use a different or new group.

Once you know the command's group, you can create the individual command. Set the trigger type (often the `Contains` type), trigger, name, response, and configure any other necessary settings.

To avoid requiring a high level of maintenance, custom command responses should ideally link to other resources instead of having detailed information directly in the bot's response.

The general format for a support command embed is demonstrated in the following command body:

```
{{ $description := `
This is the embed description.
` }}

{{ $embed := cembed
    "title" "**__This is the embed title__**"
    "description" $description
    "color" 0x000000
}}

{{ sendMessage nil $embed }}
```
> [!NOTE]
>
> Due to the use of backticks as string delimiters in the description, I don't think backticks can be used (afaik there's no way to escape the string). But I believe you can use other types of string delimiters, such as double-quotes, which will allow you to use backticks in the description.

Here is a sample custom command:

<img src="/assets/sample_custom_command.png" width="800"/>

<img src="/assets/custom_command_response.png" width="400"/>

After creating a custom command, the command trigger and description should be added to the list of custom commands in [`#⁠🆘・quick-support`](https://discord.com/channels/1270729807948415048/1270739900752461845/1280014426963185698). This list provides helpers and troubled users the information they need to use the commands effectively.

The list of custom commands is a webhook message, so refer to the previous part on editing webhook messages.



# GitHub notifications
The webhook messages in ⁠`#💻・github` are sent by GitHub actions in each repository, which are triggered upon any release. (The file path for the workflow is in `.github/workflows`)

The webhook URL is stored in each repository as a repository secret.

If for some reason an update fails to send, it can ofc be done manually. 



# YAGPDB automod
The automod is configured at https://yagpdb.xyz/manage/1270729807948415048/automod/. The main ruleset has basic functionality, such as spam protection and deleting links from `revanced.net` and similar popular sites.

If users trigger the automod too many times within a set interval, they will be placed in timeout. Further violations will result in a ban.



# Making announcements
Announcements should be mirrored from the announcements Telegram channel (https://t.me/revanced_extended) and include other important matters. 

When making an announcement, the `@🔔 Announcements` role should be mentioned, and the message should be published so that people who follow ⁠`#🔔・announcements` in their server will get the message.

The `@Auto Publisher 3` bot should automatically publish all messages sent in ⁠`#🔔・announcements` and `#⁠💻・github` . 

If the bot is offline, messages will need to be published manually. To publish an announcement on mobile, simply hold down on the message and press "Publish". To publish an announcement from desktop, hover over the message and click the 📣 emoticon.

<img src="//assets/publish.png" width="400"/>

# Auto publishing bot
`@Auto Publisher 3 is a bot that will automatically publish messages sent in an announcement channel as long as it has the permissions to do so. According to the configuration instructions, the following permissions should be given to the bot in the announcement channel:

`View Channel`, `Send Messages`, `Manage Messages`, and `Read Message History`.
