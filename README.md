# Boilerplate Docker Node.js

Boilerplate com arquivos para rodar a aplicação **Node.js** via **docker**.

Utilizados nos projetos:

- [Boilerplate Rest](https://github.com/lagden/boilerplate-rest)
- [Boilerplate GraphQL](https://github.com/lagden/boilerplate-gql)
- [Boilerplate Svelte](https://github.com/lagden/boilerplate-svelte)


## Como usar

⚠️ **Atenção!**

Esses arquivos dependem de uma estrutura específica para que funcionem adequadamente.

**Exemplo:**

```
npx degit lagden/boilerplate-gql#main meu_app
cd meu_app
npx degit lagden/boilerplate-bin/files#main bin
npx degit lagden/boilerplate-envs/files#main ./ --force
npx degit lagden/boilerplate-docker-nodejs/files#main ./ --force
```

---

Caso utilize para aplicações **frontend**, faça o seguinte:

- Apague o `Dockerfile`
- Renomeie o  arquivo `Dockerfile.front` para `Dockerfile`


## License

MIT © [Thiago Lagden](https://github.com/lagden)
