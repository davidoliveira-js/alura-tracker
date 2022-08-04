<template>
  <section>
    <form @submit.prevent="salvar">
      <div class="field">
        <label for="nomeDoProjeto" class="label"> Nome do Projeto </label>
        <input
          type="text"
          class="input"
          v-model="nomeDoProjeto"
          id="nomeDoProjeto"
        />
      </div>
      <div class="field">
        <button class="button" type="submit">Salvar</button>
      </div>
    </form>
  </section>
</template>

<script lang="ts">
import { TipoNotificacao } from "@/interfaces/INotificacao";
import { ADICIONA_PROJETO, ALTERA_PROJETO } from "@/store/tipo-mmutacoes";
import { defineComponent } from "vue";
import { useStore } from "../../store/index";
import useNotificador from "@/hooks/notificador";

export default defineComponent({
  name: "FormularioVue",
  data() {
    return {
      nomeDoProjeto: "",
    };
  },
  mounted() {
    if (this.id_projeto) {
      const projeto = this.store.state.projetos.find(
        (proj) => proj.id == this.id_projeto
      );
      this.nomeDoProjeto = projeto?.nome || "";
    }
  },
  props: {
    id_projeto: {
      type: String,
    },
  },
  methods: {
    salvar() {
      if (this.id_projeto) {
        this.store.commit(ALTERA_PROJETO, {
          id: this.id_projeto,
          nome: this.nomeDoProjeto,
        });
      } else {
        this.store.commit(ADICIONA_PROJETO, this.nomeDoProjeto);
      }
      this.notificar(
        TipoNotificacao.SUCESSO,
        "SALVO",
        "Item salvo com sucesso"
      );
      this.nomeDoProjeto = "";
      this.$router.push("/projetos");
    },
  },
  setup() {
    const store = useStore();
    const { notificar } = useNotificador();
    return {
      store,
      notificar,
    };
  },
});
</script>

