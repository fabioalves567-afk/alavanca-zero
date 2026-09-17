# ALAVANCA ZERO — Fahrwerk SmartFlow + Firebase + GitHub Pages + PIN do Monitor

## Modelo de acesso

- Operador: questionário público e anônimo.
- Monitor: informa **somente um PIN de 4 números**.
- O PIN é autenticado pelo Firebase Authentication.
- O PIN não é armazenado no Firestore.
- Dentro da área do Monitor existe o botão **🔐 PIN** para alterar o PIN.
- Para alterar, o monitor informa PIN atual + novo PIN + confirmação.

## Projeto Firebase configurado

Projeto: `fahrwerk-smartflow`

## Configuração inicial no Firebase

1. Crie/abra o projeto no Firebase.
2. Ative **Firestore Database**.
3. Ative **Authentication > Sign-in method > Email/Password**.
4. Crie um usuário no Authentication com:
   - E-mail técnico: `monitor@alavanca-zero.app`
   - Senha inicial: `ALZ-1234`

   O monitor não verá nem precisará informar esse e-mail. O aplicativo transforma o PIN digitado em uma senha técnica para o Firebase.

5. Copie o UID desse usuário.
6. No Firestore, crie:
   - coleção: `users`
   - documento: `UID_DO_USUARIO`
   - campo: `role` = `monitor`

7. Em `index.html`, substitua apenas os valores de `firebaseConfig` pelos dados do seu Web App do Firebase.

## Regras do Firestore

Publique `firestore.rules`:

```bash
firebase deploy --only firestore:rules
```

A coleção `diagnosticos_alavanca` pode receber respostas anônimas, mas somente um usuário autenticado com `role: monitor` pode ler, editar ou excluir respostas.

## GitHub Pages

Envie `index.html`, `firebase.json`, `firestore.rules` e `.gitignore` para o repositório.

Depois, no GitHub:
**Settings → Pages → Deploy from a branch → main → / (root)**.

## Importante

Não coloque service account JSON, chave privada ou senha administrativa no GitHub.

O `firebaseConfig` do aplicativo web pode aparecer no código público; a proteção real fica nas regras do Firestore e no Firebase Authentication.
