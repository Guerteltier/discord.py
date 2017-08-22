# discord.py scrumpy version

This is not the offical version of Discord.py, this is a personal build to be used until I need to move to rewrite myself.
You can find the offical version over here: https://github.com/Rapptz/discord.py/

### About upgrading

Do note that installing this package will remove the official version of dPy from your box, although I do plan to make sure I keep this repo up to date with the official one do keep this in mind that if I suddenly dissapear you might not get updates.

## Installing

To install the library without full voice support, you can just run the following command:

```
python3 -m pip install git+https://github.com/KakolIsSomewhatGay/discord.py@async
# If there was a supar important update and I forgot to change the version number append `--upgrade` to the end to force the update.
```


Otherwise to get voice support you should run the following command:

```
python3 -m pip install git+https://github.com/KakolIsSomewhatGay/discord.py@async[voice]
```

To install the development version, do the following:

```
python3 -m pip install -U https://github.com/KakolIsSomewhatGay/discord.py/archive/master.zip#egg=discord.py[voice]
```

or the more long winded from cloned source:

```
$ git clone https://github.com/KakolIsSomewhatGay/discord.py
$ cd discord.py
$ python3 -m pip install -U .[voice]
```

Please note that on Linux installing voice you must install the following packages via your favourite package manager (e.g. `apt`, `yum`, etc) before running the above command:

- libffi-dev (or `libffi-devel` on some systems)
- python<version>-dev (e.g. `python3.5-dev` for Python 3.5)

## Quick Example

```py
import discord
import asyncio

client = discord.Client()

@client.event
async def on_ready():
    print('Logged in as')
    print(client.user.name)
    print(client.user.id)
    print('------')

@client.event
async def on_message(message):
    if message.content.startswith('!test'):
        counter = 0
        tmp = await client.send_message(message.channel, 'Calculating messages...')
        async for log in client.logs_from(message.channel, limit=100):
            if log.author == message.author:
                counter += 1

        await client.edit_message(tmp, 'You have {} messages.'.format(counter))
    elif message.content.startswith('!omgverynsfwcommand'):
        await asyncio.sleep(5)
        if message.channel.is_nsfw is True:
            is_nsfw_omg = "is not"
        elif:
            is_nsfw_omg = "is"

        await client.send_message(message.channel, 'The channel {0} nsfw'.format(
            is_nsfw_omg
        ))

client.run('token')
```

Note that in Python 3.4 you use `@asyncio.coroutine` instead of `async def` and `yield from` instead of `await`.

You can find examples in the examples directory.

## Requirements

- Python 3.4.2+
- `aiohttp` library
- `websockets` library
- `PyNaCl` library (optional, for voice only)
    - On Linux systems this requires the `libffi` library. You can install in
      debian based systems by doing `sudo apt-get install libffi-dev`.

Usually `pip` will handle these for you.

## Related Projects

- [discord.py](https://github.com/Rapptz/discord.py/)
- [discord.js](https://github.com/discord-js/discord.js)
- [discord.io](https://github.com/izy521/discord.io)
- [Discord.NET](https://github.com/RogueException/Discord.Net)
- [DiscordSharp](https://github.com/Luigifan/DiscordSharp)
- [Discord4J](https://github.com/knobody/Discord4J)
- [discordrb](https://github.com/meew0/discordrb)
