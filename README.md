# Rede Consciente - GitHub Pages

Arquivo principal: `index.html`.

## Como publicar

1. Crie um repositório no GitHub, por exemplo: `rede-consciente`.
2. Envie o arquivo `index.html` para a raiz do repositório.
3. Vá em `Settings > Pages`.
4. Em `Build and deployment`, escolha `Deploy from a branch`.
5. Selecione `main` e `/root`.
6. Salve.

O site ficará em algo como:

`https://SEU_USUARIO.github.io/rede-consciente/`

## Configuração obrigatória no Firebase

1. Crie um projeto no Firebase.
2. Ative `Authentication > Sign-in method > Google`.
3. Ative `Firestore Database`.
4. No Firebase, copie os dados do app Web e cole no bloco `firebaseConfig` do `index.html`.
5. Em `Authentication > Settings > Authorized domains`, adicione:

`SEU_USUARIO.github.io`

## Regras sugeridas para teste escolar no Firestore

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /posts/{postId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update: if request.auth != null;
      allow delete: if request.auth != null && (
        request.auth.token.email == resource.data.authorEmail
        || request.auth.token.email in ['COLOQUE_SEU_EMAIL_AQUI@gmail.com']
      );
    }
  }
}
```
