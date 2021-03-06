![alt text](https://i.imgur.com/U4niq5L.png "Gorilink")
[![Version](https://badgen.net/npm/v/gorilink)](https://www.npmjs.com/package/gorilink)
![License](https://badgen.net/github/license/micromatch/micromatch)

## Easy lavalink wrapper for Discord.js. (soon Eris)

# Documentation
Documentation soon...

# How to install
### Using yarn:
**`yarn add gorilink`**
### Using npm:
**`npm install gorilink`**

# How to use
You need have [Lavalink](https://github.com/Frederikam/Lavalink) node instance.

## Example
```javascript
// Importing Discord.js Client
const { Client } = require('discord.js')
// Importing GorilinkManager
const { GorilinkManager } = require('gorilink')

// Your lavalink node config
const nodes = [
  {
    tag: 'Node 1', // optional
    host: 'localhost',
    port: 2333,
    password: 'youshallnotpass'
  }
]

// Instantiating discord.js client
const client = new Client()

client.on('ready', async () => {
  // Creating GorilinkManager
  client.music = new GorilinkManager(client, config.nodes)
    // Listens events
    .on('nodeConnect', node => {
      console.log(`${node.tag || node.host} - Lavalink connected with success.`)
    })
    .on('trackStart', event => {
      event.player.textChannel.send(`Now playing \`${res.track.info.title}\``)
    })

  console.log('Online on the client', client.user.username)
})


client.on('message', async (message) => {
  const prefix = '!'
  const args = message.content.slice(prefix.length).trim().split(/ +/g)
  const cmd = args.shift().toLowerCase()

  if (cmd === 'play') {
    // Spawning lavalink player
    const player = await client.music.join({
      guild: message.guild.id,
      voiceChannel: message.member.voice.channel.id,
      textChannel: message.channel
    })

    // Getting tracks
    const { tracks } = await client.music.fetchTracks(args.join(' '))

    // Adding in queue
    player.queue.add(tracks[0])

    message.channel.send('Added in queue: ' + tracks[0].info.title)
    
    // Playing
    if (!player.playing) return player.play()
  }
})

// Logging the bot
client.login('your-token')
```

## Authors
  - Psykka
  - zMigueel
  - DerpyXD
