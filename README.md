# ⚡ TechMemory - Sistema de Estudos na Nuvem

Sistema completo de gerenciamento de estudos com sincronização na nuvem via Firebase.

## 🚀 Funcionalidades

- 📝 **Anotações** - Crie, edite e proteja suas notas
- ✅ **Tarefas** - Gerencie suas tarefas com prioridades
- 🚀 **Projetos** - Organize seus projetos
- 🔖 **Bookmarks** - Salve sites importantes
- 💡 **Ideias de Estudo** - Registre suas ideias
- 🔒 **Cofre Pessoal** - Proteja informações sensíveis com senha
- 🏷️ **Etiquetas** - Organize com tags
- 🔍 **Busca Global** - Encontre qualquer coisa rapidamente
- 📈 **Estatísticas** - Acompanhe seu progresso

## 📋 Pré-requisitos

- [Firebase Account](https://console.firebase.google.com)
- [GitHub Account](https://github.com)
- [Netlify Account](https://app.netlify.com) (para deploy)

## 🔧 Configuração do Firebase

1. Acesse o [Firebase Console](https://console.firebase.google.com)
2. Crie um novo projeto
3. Ative os seguintes serviços:
   - **Authentication** > Email/Password + Google
   - **Cloud Firestore** > Criar banco de dados

4. Vá em **Project Settings** > **General** > **Your apps** > Adicione um app Web
5. Copie a configuração e cole em `js/firebase-config.js`

6. No Firestore, crie as regras de segurança:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## 📁 Estrutura do Projeto

```
memory/
├── index.html          # Página principal
├── css/
│   └── styles.css      # Estilos
├── js/
│   ├── firebase-config.js  # Configuração Firebase
│   └── app.js          # Lógica da aplicação
├── .gitignore
└── README.md
```

## 🚀 Deploy

### GitHub + Netlify

1. Crie um repositório no GitHub
2. Faça push do código:
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/SEU-USER/techmemory.git
git push -u origin main
3. Acesse o Netlify
4. Clique em "New site from Git"
5. Selecione o repositório GitHub
6. Configure:
   - Build command: (deixe vazio)
   - Publish directory: . ou /
7. Clique em "Deploy site"

### Netlify config

- Arquivo de configuração adicionado: [netlify.toml](netlify.toml)
  - Publica a raiz do repositório (`publish = "."`).
  - Redireciona todas as rotas para `index.html` para suportar SPA.

### Próximos passos

- Faça push para o repositório GitHub e conecte no Netlify (New site from Git).
- Se quiser deploy via CLI, instale a Netlify CLI e rode:

```bash
npm install -g netlify-cli
netlify deploy --prod --dir=.
```

## 📱 Uso no Telemóvel

O app é totalmente responsivo e funciona bem em dispositivos móveis. Para uma experiência nativa:

1. Abra o site no navegador do telemóvel
2. No Chrome: toque nos 3 pontinhos > "Adicionar à tela inicial"
3. No Safari (iOS): toque no ícone de compartilhar > "Adicionar à Tela de Início"

## 🔐 Segurança

- Senhas são criptografadas pelo Firebase Auth
- Cada usuário só acessa seus próprios dados
- O Cofre usa criptografia XOR com senha do usuário
- Dados sincronizados em tempo real na nuvem

## 🛠️ Tecnologias

- HTML5 / CSS3 / JavaScript Vanilla
- Firebase Authentication
- Cloud Firestore
- Design responsivo (Mobile First)
