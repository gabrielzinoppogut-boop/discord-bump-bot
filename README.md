# Discord Bump Bot 🤖

Bot Discord que executa o comando `/bump` automaticamente a cada **2 horas** em um canal específico.

## 📋 Pré-requisitos

- Node.js v18.0.0 ou superior
- Uma aplicação Discord (Bot) criada no [Discord Developer Portal](https://discord.com/developers/applications)
- Token do bot Discord

## 🚀 Instalação

### 1. Clone o repositório
```bash
git clone https://github.com/gabrielzinoppogut-boop/discord-bump-bot.git
cd discord-bump-bot
```

### 2. Instale as dependências
```bash
npm install
```

### 3. Configure o token
Crie um arquivo `.env` na raiz do projeto:
```bash
cp .env.example .env
```

Edite o arquivo `.env` e adicione seu token do Discord:
```env
DISCORD_TOKEN=seu_token_aqui
```

### 4. Inicie o bot
```bash
npm start
```

Você verá uma mensagem como:
```
✅ Bot conectado como: seu_bot#0000
🤖 Bot está pronto para usar!
✅ Comandos slash registrados com sucesso!
```

## 📖 Como Usar

### Comandos Disponíveis

#### `/bump-start`
Inicia o bump automático a cada 2 horas no canal atual.

**Uso:**
```
/bump-start
```

**Resposta:**
```
✅ Bump automático iniciado! Será executado a cada 2 horas.
```

#### `/bump-stop`
Para o bump automático no canal atual.

**Uso:**
```
/bump-stop
```

**Resposta:**
```
⏹️ Bump automático parado!
```

#### `/bump-status`
Verifica o status do bump automático no canal atual.

**Uso:**
```
/bump-status
```

**Resposta:**
```
✅ Bump automático está ATIVO neste canal
```
ou
```
❌ Bump automático está INATIVO neste canal
```

## ⚙️ Configuração do Bot Discord

### 1. Crie uma Aplicação
1. Acesse [Discord Developer Portal](https://discord.com/developers/applications)
2. Clique em "New Application"
3. Dê um nome à sua aplicação

### 2. Crie um Bot
1. Na seção "SETTINGS", clique em "Bot"
2. Clique em "Add Bot"
3. Copie o **TOKEN** (use esse token no `.env`)

### 3. Defina Permissões
1. Na seção "OAuth2 > URL Generator"
2. Selecione os escopos:
   - `bot`
3. Selecione as permissões:
   - ✅ Send Messages
   - ✅ Use Slash Commands
   - ✅ Read Message History

4. Copie a URL gerada e acesse-a para convidar o bot ao seu servidor

### 4. Permissões no Servidor
Certifique-se de que o bot tem permissão para enviar mensagens no canal onde o bump será executado.

## 📝 Estrutura do Projeto

```
discord-bump-bot/
├── bot.js              # Código principal do bot
├── package.json        # Dependências do projeto
├── .env.example        # Exemplo de variáveis de ambiente
├── .gitignore          # Arquivos ignorados pelo Git
└── README.md           # Este arquivo
```

## 🔧 Desenvolvimento

Para desenvolvimento com auto-reload:
```bash
npm run dev
```

Isso requer o `nodemon` já instalado como devDependency.

## 📚 Dependências

- **discord.js**: Biblioteca para interagir com a API do Discord
- **dotenv**: Carrega variáveis de ambiente do arquivo `.env`

## ⚠️ Notas Importantes

- O bot deve ter permissão para enviar mensagens no canal
- O intervalo de 2 horas é definido em milissegundos: `7200000 ms`
- Se você quiser alterar o intervalo, modifique o valor em `bot.js` na linha do `setInterval`
- Os bumps são armazenados em memória; se o bot reiniciar, os intervals serão perdidos

## 🐛 Troubleshooting

### Bot não conecta
- Verifique se o token está correto no `.env`
- Certifique-se de que o bot foi criado no Developer Portal

### Comandos slash não aparecem
- Aguarde alguns minutos após iniciar o bot
- Tente usar `/` no Discord para recarregar a lista de comandos
- Verifique as permissões do bot no servidor

### Bot não envia mensagens
- Verifique se o bot tem permissão de "Send Messages" no canal
- Certifique-se de que o canal existe e o bot tem acesso

## 📄 Licença

MIT

## 💡 Sugestões e Melhorias

Sinta-se livre para fazer fork, criar branches e enviar pull requests com melhorias!

---

**Feito com ❤️ por gabrielzinoppogut-boop**
