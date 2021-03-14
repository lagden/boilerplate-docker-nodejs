# Boilerplate Docker Node.js

Boilerplate com arquivos para rodar a aplicação **Node.js** via **docker**.

Utilizados nos projetos:

- [Boilerplate Rest](https://github.com/lagden/boilerplate-rest)
- [Boilerplate GraphQL](https://github.com/lagden/boilerplate-gql)
- [Boilerplate Svelte](https://github.com/lagden/boilerplate-svelte)


## Como usar

⚠️ **Atenção**

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

Caso utilize para aplicações **frontend**, é importante ajustar os `Dockerfiles`.

```
rm Dockerfile
rm Dockerfile.dev
mv Dockerfile.front Dockerfile
mv Dockerfile.dev.front Dockerfile.dev
```


## License

MIT © [Thiago Lagden](https://github.com/lagden)
