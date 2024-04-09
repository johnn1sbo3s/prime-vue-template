# Nuxt + TailwindCSS + PrimeVue

**Este projeto já está configurado e pronto para uso. Apenas clone o repositório e instale as dependências**
``` bash
npm install
```

**A documentação a seguir é um guia para a instalação das 3 dependências a partir do zero.**

## Inicialização de um novo projeto

Considerando que o Nuxt já está instalado, crie um novo projeto a partir do CLI do Nuxt, usando:

```bash
npx nuxi@latest init <nome-do-projeto>
```

## Instale o PrimeVue Styled a partir do [tutorial oficial](https://primevue.org/nuxt/).

Instalando o PrimeVue

```bash
npm install primevue
npm install --save-dev nuxt-primevue
```

Adicione o módulo do PrimeVue ao arquivo **nuxt.config.ts**
``` bash
export default defineNuxtConfig({
    modules: [
        'nuxt-primevue'
    ],
    primevue: {
        /* Options */
    }
})
```

Entre os [temas disponíveis](https://primevue.org/theming/) no PrimeVue, adicione o de sua escolha no mesmo arquivo **nuxt.config.ts**
``` bash
export default defineNuxtConfig({
    modules: [
        'nuxt-primevue'
    ],
    primevue: {
        /* Options */
    },
    css: ['primevue/resources/themes/aura-light-green/theme.css'],
})
```

A partir de agora, os componentes do PrimeVue já estão disponíveis para uso.
``` bash
<Button label="Click me!" />
```

Agora, vamos instalar o Tailwind CSS.

## Instalando o Tailwind CSS

Seguindo a [documentação oficial](https://tailwindcss.com/docs/guides/nuxtjs#standard), começamos a instalação com os seguintes comandos:
``` bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

Adicione o Tailwind à configuração de postcss.plugins no arquivo **nuxt.config.ts**
``` bash
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  devtools: { enabled: true },
  postcss: {
    plugins: {
      tailwindcss: {},
      autoprefixer: {},
    },
  },
})
```

Adicione todos os caminhos de template no arquivo **tailwind.config.js**
``` bash
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./components/**/*.{js,vue,ts}",
    "./layouts/**/*.vue",
    "./pages/**/*.vue",
    "./plugins/**/*.{js,ts}",
    "./app.vue",
    "./error.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Crie uma pasta **assets/css** e um arquivo **main.css** dentro dela, com o seguinte código:
``` bash
@layer tailwind-base {
  @tailwind base;
}

@layer tailwind-utilities {
  @tailwind components;
  @tailwind utilities;
}
```

Adicione o caminho à configuração de CSS no arquivo **nuxt.config.ts**
``` bash
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: ["nuxt-primevue"],
  primevue: {
    /* Options */
  },
  css: [
    "~/assets/css/main.css",
    "primevue/resources/themes/aura-light-green/theme.css",
  ],
  ...
```

Finalmente, adicione o CSSLayer do PrimeVue ao arquivo de configuração **nuxt.config.ts**
``` bash
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: ["nuxt-primevue"],
  primevue: {
    cssLayerOrder: "tailwind-base, primevue, tailwind-utilities",
  },
  ...
```

Ao final de tudo, teremos um **nuxt.config.ts** assim:
``` bash
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: ["nuxt-primevue"],
  primevue: {
    cssLayerOrder: "tailwind-base, primevue, tailwind-utilities",
  },
  css: [
    "~/assets/css/main.css",
    "primevue/resources/themes/aura-light-green/theme.css",
  ],
  postcss: {
    plugins: {
      tailwindcss: {},
      autoprefixer: {},
    },
  },
});
```

E pronto! Nosso projeto já está configurado, usando Nuxt, TailwindCSS e PrimeVue.
