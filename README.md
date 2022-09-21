# Apex Legends Map Bot 

### Replit Link: https://replit.com/
### Apex Legends API: https://apexlegendsapi.com/
### Discord Dev Portal: https://discord.com/developers/docs/intro

## List of Packages Needed:
- python = "^3.8"
- discord = "^1.7.3"
- poetry = "^1.1.8"
- json5 = "^0.9.6"
- requests = "^2.26.0"
- http_request = "^1.2"
- "discord.py" = "^1.7.3"
- discord-cli = "^1.0.0"

# Code
```
import os
import requests
import json
import discord
from discord.ext import commands


client = commands.Bot(command_prefix=commands.when_mentioned_or("d/","D/"),help_command=None)

#api key references 
my_secret = os.environ['TOKEN']
apiSecret = os.environ['apexApi']

#notify me when bot has come online
@client.event
async def on_ready():
  print('bot is now online!!!!')


@client.event 
async def on_message(message):
  msg_content = message.content.lower()


  #bot command
  atCommandMap = ["!map"]


  if any(word in msg_content for word in atCommandMap):
    r = requests.get(f"https://api.mozambiquehe.re/maprotation?version=2&auth={apiSecret}")

    if r is None: 
      print("api is not working")
    else:
      j=r.json()

      #battleRoyale Maps
      currentMapName = j["battle_royale"]["current"]["map"]
      nextMapName = j["battle_royale"]["next"]["map"]
      timeRemaining = j["battle_royale"]["current"]["remainingMins"]


      await message.channel.send(f"Current Map: {currentMapName}\nNext Map: {nextMapName}\nTime Remaining: {timeRemaining}")

client.run(my_secret)
```
