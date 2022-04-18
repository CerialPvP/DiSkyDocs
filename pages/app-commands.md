# Application Commands

> :warning: Before reading the rest of the tutorial, check out [Installation](https://disky.tech/wiki/?page=install), [Bot Creation](https://disky.tech/wiki/?page=bot-creation) and [Bot Loading](https://disky.tech/wiki/?page=bot-loading).

**Application Commands**, or more commonly known as **Slash Commands**, are commands used in Discord which are prefixed with a slash `/`. Slash commands offer:

* 9 options
* Default options
* And more!
  
We will be showcasing them and learning how to make them.

### How to make slash commands?

It's quite simple. You can put the example code everywhere (including commands, events, ect), but we personally recommend putting them in an `on load` event, so every time you reload your script, the commands will update.

Here is how to make a slash command:
```applescript
# Replace the command name and description to your liking.
set {_c} to new slash command named "commandname" with description "This is a very epic command!"
```

Let's get to options. They are like Skript arguments, but more custom. You can also make them optional, which means you don't have to put them in the slash command. Here are all option types explained.

| Option Type | What it does |
| ------ | ------------ |
| string | You can enter anything in there. |
| integer | You can enter only a **rounded number** in there. This means no decimals (for example 3.4). |
| number | You can enter any number **including numbers with decimals**. |
| boolean | You can only specify `True` or `False` in there.
| user | You can search and select a user from the server you're executing the slash command from. |
| role | Pretty much the same thing above, but instead for roles. |
| channel | Pretty much the same thing above, but instead for channels. |

Let's say I want to make a command to get the Discord ID of a user. We have to add the `user` option type to get the user. We are going to put `required` before the option type to make the option required to enter. This is the current command now:
```applescript
set {_c} to new slash command named "getuserid" with description "Gets the Discord ID of a user."
add required user option named "user" with description "The user which you want to get their ID." to options of {_c}
```

Now, we need to register the command, so it will be visible.

There are 2 ways; either registering it in a specific guild (Discord server) or globally (in all guilds the bot is in.)

> :warning: Note 1: Make sure the server(s) invited the bot with the `application.commands` scope and with the `Use Slash Commands` permission, otherwise the bot won't be able to register the slash commands. This can be seen in the GIF below.
![Bot Invite](https://i.imgur.com/j2crGMW.gif)

> :warning: Note 2: If you register slash commands globally, it will take an hour to register in all servers. If you want to develop the slash command, we recommend testing it in a test server, then once you're done, make it global.

Here is how to register it locally:
```applescript
update command {_c} locally in guild with id "GUILD_ID"
```

And here is how to register it globally:
```applescript
update command {_c} globally in bot "BOT_NAME"
```

Let's say we want to register the command we created above in all guilds, this is how the command will look now:
```applescript
set {_c} to new slash command named "getuserid" with description "Gets the Discord ID of a user."
add required user option named "user" with description "The user which you want to get their ID." to options of {_c}
update command {_c} globally in bot "User Utilities"
```

Congrats! You have made a slash command! But now, you will see something like this:
![application didn't respond](https://i.imgur.com/CqhiaJ5.gif)

Now, this is happening because DiSky can't do anything about it since there is no code that will happen after the command is executed.

### How to make the slash command execute code?

You can execute anything in a slash command. First, we need to detect when a slash command is used and if the slash command used is the one we want to make the code for.

Now, we made a command to get a user's Discord ID, so let's detect the command.
```applescript
on slash command:
    event-string = "getuserid"
```

**"getuserid"** is the command we want to execute the code for. Below that, feel free to enter any code you'd like.

Now, we want to get the argument, so to do that, we do:
```applescript
#  Make sure to put the option type you used for your command here
#                                  ↓
set {_user} to argument "user" as user
#                                  ↑
```

Make sure you put the correct option type we defined above so this will work correctly.

Now, let's reply with the ID of the user. The code should be looking like this:
```applescript
on slash command:
    event-string = "getuserid"

    set {_user} to argument "user" as user
    reply with "%mention tag of {_user}%'s ID is `%discord id of {_user}%`!"
```

Now, the slash command will reply with this:
![final result](https://i.imgur.com/24bXteH.gif)

Thanks for tuning in with us! Hope you will enjoy using DiSky!