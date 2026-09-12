const { Client, GatewayIntentBits, ChannelType } = require('discord.js');
require('dotenv').config();

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent,
    GatewayIntentBits.DirectMessages
  ]
});

// Armazena os intervalos ativos
const activeIntervals = new Map();

client.once('ready', () => {
  console.log(`✅ Bot conectado como: ${client.user.tag}`);
  console.log(`🤖 Bot está pronto para usar!`);
});

client.on('interactionCreate', async (interaction) => {
  if (!interaction.isChatInputCommand()) return;

  const { commandName, channelId, guildId } = interaction;

  if (commandName === 'bump-start') {
    // Verifica se já existe um intervalo ativo neste servidor
    const serverId = `${guildId}-${channelId}`;
     
    if (activeIntervals.has(serverId)) {
      return interaction.reply({
        content: '⚠️ Já existe um bump automático ativo neste canal!',
        ephemeral: true
      });
    }

    // Envia o primeiro bump imediatamente
    await interaction.deferReply({ ephemeral: true });
    
    try {
      const channel = await client.channels.fetch(channelId);
      await channel.send('/bump');
      await interaction.editReply('✅ Bump automático iniciado! Será executado a cada 2 horas.');

      // Define o intervalo para executar a cada 2 horas (7200000 ms)
      const intervalId = setInterval(async () => {
        try {
          await channel.send('/bump');
          console.log(`📤 Bump enviado em ${channel.name} (${guildId})`);
        } catch (error) {
          console.error(`❌ Erro ao enviar bump: ${error.message}`);
        }
      }, 7200000); // 2 horas em milissegundos

      // Armazena o intervalo
      activeIntervals.set(serverId, intervalId);
      console.log(`🔄 Bump automático iniciado no canal ${channel.name} (${serverId})`);
    } catch (error) {
      console.error(`Erro ao iniciar bump automático: ${error}`);
      await interaction.editReply('❌ Erro ao iniciar o bump automático!');
    }
  }

  if (commandName === 'bump-stop') {
    const serverId = `${guildId}-${channelId}`;
    
    if (!activeIntervals.has(serverId)) {
      return interaction.reply({
        content: '⚠️ Não há nenhum bump automático ativo neste canal!',
        ephemeral: true
      });
    }

    // Para o intervalo
    clearInterval(activeIntervals.get(serverId));
    activeIntervals.delete(serverId);

    await interaction.reply({
      content: '⏹️ Bump automático parado!',
      ephemeral: true
    });
    console.log(`⏹️ Bump automático parado no canal ${serverId}`);
  }

  if (commandName === 'bump-status') {
    const serverId = `${guildId}-${channelId}`;
    const isActive = activeIntervals.has(serverId);

    const status = isActive 
      ? '✅ Bump automático está **ATIVO** neste canal' 
      : '❌ Bump automático está **INATIVO** neste canal';

    await interaction.reply({
      content: status,
      ephemeral: true
    });
  }
});

// Registra os comandos slash quando o bot se conecta
client.on('ready', async () => {
  try {
    const commands = [
      {
        name: 'bump-start',
        description: 'Inicia o bump automático a cada 2 horas neste canal'
      },
      {
        name: 'bump-stop',
        description: 'Para o bump automático neste canal'
      },
      {
        name: 'bump-status',
        description: 'Verifica o status do bump automático neste canal'
      }
    ];

    await client.application.commands.set(commands);
    console.log('✅ Comandos slash registrados com sucesso!');
  } catch (error) {
    console.error('❌ Erro ao registrar comandos:', error);
  }
});

client.login(process.env.DISCORD_TOKEN);
