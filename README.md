# Meta do Motorista

Aplicação web para motoristas de aplicativo calcularem quanto precisam ganhar por mês, semana e dia para pagar as contas, e acompanharem o progresso. Os dados ficam na nuvem (Firebase), separados mês a mês, e sincronizam entre celular e computador.

## Funcionalidades

- Login com Google ou e-mail e senha
- Contas mensais com vencimento, e metas mensal, semanal e diária
- Meta do dia recalculada conforme o que você já ganhou
- Registro de ganhos (bruto, gastos e horas)
- Cada mês guarda suas próprias contas: mudar as contas não altera o histórico
- Funciona sem internet e sincroniza quando a conexão volta
- Backup em arquivo JSON

## Estrutura dos dados (Firestore)

```
usuarios/{uid}                 → cfg (dias de trabalho, margem) e contasPadrao
usuarios/{uid}/meses/{AAAA-MM} → contas, cfg e ganhos daquele mês
```

## Configurar o Firebase (uma vez)

1. Acesse https://console.firebase.google.com e clique em **Criar projeto**. O Google Analytics é opcional.
2. **Authentication → Começar**. Em *Sign-in method*, ative **Google** e **E-mail/senha**.
3. **Firestore Database → Criar banco de dados**. Escolha a região `southamerica-east1 (São Paulo)` e o **modo de produção**.
4. Na aba **Regras** do Firestore, apague o conteúdo, cole o do arquivo `firestore.rules` e clique em **Publicar**.
5. Em **⚙️ Configurações do projeto → Seus apps**, clique no ícone **</>** (Web), dê um nome e registre. Copie o objeto `firebaseConfig` para o arquivo `firebase-config.js`.
6. Em **Authentication → Settings → Authorized domains**, adicione `SEU-USUARIO.github.io`. O `localhost` e o `127.0.0.1` já vêm autorizados para testes.

## Rodar localmente

O app usa módulos JavaScript, então não abre com clique duplo no arquivo. Use o **Live Server** do VS Code, ou:

```bash
python3 -m http.server 8000
```

## Publicar

GitHub Pages: **Settings → Pages → Deploy from a branch → main / (root)**.
