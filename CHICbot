const { Client, Intents } = require('discord.js');
const fetch = require('node-fetch');

const client = new Client({
  intents: [
    Intents.FLAGS.GUILDS,
    Intents.FLAGS.GUILD_MESSAGES,
    Intents.FLAGS.GUILD_VOICE_STATES,
  ],
});

// Event: Bot is ready
client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}`);
});

// Event: Message received
client.on('messageCreate', async (message) => {
  // Check if the message starts with a specific prefix (e.g., "!")
  if (message.content.startsWith('!')) {
    // Extract the command and arguments from the message
    const [command, ...args] = message.content.slice(1).split(' ');

    // Perform actions based on the command
    if (command === 'hello') {
      message.reply('Hello, I am your bot!');
    } else if (command === 'ping') {
      message.reply('Pong!');
    } else if (command === 'say') {
      const text = args.join(' ');
      message.channel.send(text);
    } else if (command === 'buttonClicked') {
      const hasNFT = await checkHasNFT(message.author.id);
      if (hasNFT) {
        const targetChannelId = '1114844063376625725';
        const targetChannel = client.channels.cache.get(targetChannelId);

        if (targetChannel && targetChannel.isVoice()) {
          targetChannel
            .join()
            .then((connection) => {
              console.log('Player has entered the Discord room.');
            })
            .catch((error) => {
              console.error(`Failed to connect to the voice channel: ${error}`);
            });
        } else {
          console.error('Invalid target channel or target channel is not a voice channel.');
        }
      } else {
        console.log('Player does not have the required NFT.');
      }
    } // Add more commands and functionality as needed
  }
});

// Function: Check if the player has the required NFT
async function checkHasNFT(playerId) {
  // Replace with your NFT contract address and token ID
  const nftContractAddress = '0x2953399124F0cBB46d2CbACD8A89cF0599974963';
  const nftTokenId = '45856530773552541248370019998774437862079317400988178320254074132141906591844';

  const openSeaAPIUrl = `https://api.opensea.io/api/v1/assets?owner=${playerId}&asset_contract_address=${nftContractAddress}&token_ids=${nftTokenId}`;

  try {
    const response = await fetch(openSeaAPIUrl);
    const data = await response.json();

    return data.assets.length > 0;
  } catch (error) {
    console.error(`Failed to fetch NFT data: ${error}`);
    return false;
  }
}

// Log in the bot with your Discord bot token
client.login('MTEwODI5NjE5ODA0NzEzNzgyNQ.GbrqNN.RjCxttKPsTo3JZ3RAo1E3Jal5NHq1wFGGHsCaQ');
