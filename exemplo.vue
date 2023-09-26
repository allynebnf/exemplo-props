<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>exemplo de props</title>
  </head>
  <body>
    <div id="app">
      <avo :mensagem-avo="mensagemDoFilho"></avo>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@3.2.0/dist/vue.global.prod.js"></script>
    <script>
      const Filho = {
        template: `
                <div>
                    <p>Componente Filho</p>
                </div>
            `,
        data() {
          return {
            mensagemDoFilho: "Olá, sou o filho!",
          };
        },
      };

      const Pai = {
        components: {
          Filho,
        },
        template: `
                <div>
                    <p>Componente Pai</p>
                    <Filho :mensagem-filho="mensagemDoFilho"></Filho>
                </div>
            `,
        data() {
          return {
            mensagemDoFilho: "",
          };
        },
        mounted() {
          this.mensagemDoFilho = this.$refs.filho.mensagemDoFilho;
        },
      };

      const Avo = {
        props: {
          mensagemAvo: String,
        },
        template: `
                <div>
                    <p>Componente Avo</p>
                    <p>Mensagem recebida do filho: {{ mensagemAvo }}</p>
                </div>
            `,
      };

      const app = Vue.createApp({
        components: {
          Avo,
        },
        data() {
          return {
            mensagemDoFilho: "",
          };
        },
        mounted() {
          this.mensagemDoFilho = this.$refs.pai.mensagemDoFilho;
        },
      });

      app.mount("#app");
    </script>
  </body>
</html>
