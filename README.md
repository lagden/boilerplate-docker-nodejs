# Boilerplate Docker Node.js

Boilerplate para executar uma aplicação **Node.js** via **docker**.

Utilizados nos projetos:

- [Boilerplate Rest](https://github.com/lagden/boilerplate-rest)
- [Boilerplate GraphQL](https://github.com/lagden/boilerplate-gql)
- [Boilerplate Svelte](https://github.com/lagden/boilerplate-svelte)


## Como usar

⚠️ **Atenção**

Esses arquivos dependem de uma estrutura específica para que funcionem.

**Exemplo:**

```
yarn dlx degit lagden/boilerplate-rest#master meu_app
cd meu_app
yarn dlx degit lagden/boilerplate-bin/files#main bin
yarn dlx degit lagden/boilerplate-envs/files#main ./ --force
yarn dlx degit lagden/boilerplate-docker-nodejs/files#main ./ --force
```

---

Caso utilize para o desenvolvimento de aplicações **frontend**, é importante ajustar o `Dockerfile`.

```
rm Dockerfile
mv Dockerfile.front Dockerfile
```


## License

MIT © [Thiago Lagden](https://github.com/lagden)
