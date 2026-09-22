# Passo a passo: colocar o Meta do Motorista para rodar

Tempo total: cerca de 30 minutos. Faça na ordem.

---

## Parte 1: instalar as ferramentas (só na primeira vez)

1. Instale o **VS Code**: https://code.visualstudio.com
2. Instale o **Git**: https://git-scm.com (pode aceitar todas as opções padrão).
3. Crie uma conta no **GitHub**, se ainda não tiver: https://github.com
4. Abra o VS Code, vá em **Terminal → Novo Terminal** e rode (troque pelos seus dados):

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

---

## Parte 2: abrir o projeto no VS Code

1. Descompacte o `meta-motorista.zip` numa pasta fácil, como `Documentos/meta-motorista`.
2. No VS Code: **Arquivo → Abrir Pasta** e escolha a pasta `meta-motorista`.
3. Se aparecer "Você confia nos autores dos arquivos?", clique em **Sim, confio**.
4. Vai aparecer um aviso recomendando a extensão **Live Server**. Clique em **Instalar**.
   (Se não aparecer: Extensões `Ctrl + Shift + X` → pesquise "Live Server" de Ritwick Dey → Instalar.)

---

## Parte 3: criar o Firebase (banco de dados e login)

### 3.1 Criar o projeto
1. Acesse https://console.firebase.google.com e entre com sua conta Google.
2. Clique em **Criar projeto** (ou *Adicionar projeto*).
3. Nome: `meta-motorista` → Continuar.
4. Google Analytics: pode **desativar** → Criar projeto → Continuar.

### 3.2 Ativar o login
1. No menu à esquerda: **Criação → Authentication** → **Vamos começar**.
2. Aba **Sign-in method**:
   - Clique em **Google** → ative → escolha seu e-mail de suporte → **Salvar**.
   - Clique em **Adicionar novo provedor → E-mail/senha** → ative só a primeira opção → **Salvar**.

### 3.3 Criar o banco de dados
1. No menu: **Criação → Firestore Database** → **Criar banco de dados**.
2. Local: **southamerica-east1 (São Paulo)** → Avançar.
3. Escolha **Iniciar no modo de produção** → Criar.

### 3.4 Colar as regras de segurança (importante!)
1. Ainda no Firestore, abra a aba **Regras**.
2. Apague tudo que estiver lá.
3. No VS Code, abra o arquivo `firestore.rules`, copie todo o conteúdo e cole no Firebase.
4. Clique em **Publicar**.

### 3.5 Conectar o app ao Firebase
1. Clique na engrenagem ⚙️ ao lado de "Visão geral do projeto" → **Configurações do projeto**.
2. Role até **Seus apps** e clique no ícone **</>** (Web).
3. Apelido: `meta-motorista-web`. **Não** marque Firebase Hosting → **Registrar app**.
4. Vai aparecer um código com `const firebaseConfig = { ... }`. Copie só os valores de dentro das chaves.
5. No VS Code, abra `firebase-config.js` e substitua os valores de exemplo pelos seus. Fica parecido com:

```js
export const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "meta-motorista-xxxxx.firebaseapp.com",
  projectId: "meta-motorista-xxxxx",
  storageBucket: "meta-motorista-xxxxx.firebasestorage.app",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abc123..."
};
```

6. Salve com `Ctrl + S`.

---

## Parte 4: testar no computador

1. No VS Code, com a pasta aberta, clique em **Go Live** no canto inferior direito.
2. O navegador abre o app na tela de login.
3. Entre com **Google** (ou crie uma conta com e-mail e senha).
4. Cadastre uma conta de teste em **Contas e metas** e um ganho de teste em **Hoje**.
5. Confira no Firebase: **Firestore Database → Dados**. Deve aparecer `usuarios` e, dentro, `meses`. Funcionou!

> Importante: o app **não abre** com clique duplo no `index.html`. Use sempre o Go Live para testar.

---

## Parte 5: publicar no GitHub

1. No VS Code, clique no ícone de **Controle do Código-Fonte** (`Ctrl + Shift + G`).
2. Clique em **Publicar no GitHub** (*Publish to GitHub*).
3. Autorize o login do GitHub no navegador e volte ao VS Code.
4. Escolha **Publicar em repositório público** (*public repository*).
5. Se perguntar quais arquivos incluir, deixe **todos** marcados → OK.

---

## Parte 6: colocar o site no ar (GitHub Pages)

1. Abra o repositório no GitHub (github.com/SEU-USUARIO/meta-motorista).
2. Vá em **Settings → Pages**.
3. Em *Source*: **Deploy from a branch** → branch **main** → pasta **/ (root)** → **Save**.
4. Espere 1 a 2 minutos e atualize a página. O link aparece no topo:
   `https://SEU-USUARIO.github.io/meta-motorista/`

### Autorizar o endereço no Firebase (senão o login não funciona)
1. Firebase → **Authentication → Settings → Authorized domains** (*Domínios autorizados*).
2. **Add domain** → digite `SEU-USUARIO.github.io` (sem https e sem /meta-motorista) → Adicionar.

---

## Parte 7: instalar no celular

1. Abra o link do GitHub Pages no celular e entre com a mesma conta.
2. **Android (Chrome):** menu ⋮ → **Adicionar à tela inicial** / **Instalar app**.
3. **iPhone (Safari):** botão Compartilhar → **Adicionar à Tela de Início**.

Pronto! O app fica com ícone próprio e sincroniza com o computador.

---

## Como atualizar o app no futuro

1. Altere os arquivos no VS Code e salve.
2. Teste com o **Go Live**.
3. Controle do Código-Fonte → escreva uma mensagem → **Confirmar** → **Sincronizar Alterações**.
4. Em cerca de 1 minuto o site atualiza. Se não aparecer, force com `Ctrl + F5`.

---

## Problemas comuns

| O que aparece | Como resolver |
|---|---|
| "Falta conectar ao Firebase" | O `firebase-config.js` ainda está com os valores de exemplo. Refaça o passo 3.5. |
| "Este endereço não está autorizado no Firebase" | Adicione o domínio nos Authorized domains (Parte 6). |
| "Verifique as regras do Firestore" | As regras não foram publicadas. Refaça o passo 3.4. |
| Janela do Google não abre | O navegador bloqueou o pop-up. Libere pop-ups para o site. |
| "Please tell me who you are" no Git | Faltou o comando `git config` da Parte 1. |
| Página em branco ao abrir o `index.html` direto | Use o Go Live, não o clique duplo. |
| Link do GitHub Pages dá 404 | Espere mais alguns minutos e confira se o `index.html` está na raiz do repositório. |

## Custos

O plano gratuito do Firebase (Spark) não pede cartão e sobra para uso pessoal. O GitHub Pages também é gratuito.
