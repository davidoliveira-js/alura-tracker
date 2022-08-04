<template>
  <section>
    <router-link to="/projetos/novo" class="button">
      <span class="icon is-small">
        <i class="fas fa-plus"></i>
      </span>
      <span>Novo Projeto</span>
    </router-link>
    <table class="table is-fullwidth">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>Acões</th>
        </tr>
      </thead>
      <tbody v-for="projeto in projetos" :key="projeto.id">
        <tr>
          <td>{{ projeto.id }}</td>
          <td>{{ projeto.nome }}</td>
          <td>
            <router-link :to="`/projetos/${projeto.id}`" class="button">
              <span class="icon i9s-small">
                <i class="fas fa-pencil-alt"></i>
              </span>
            </router-link>
            <button class="button ml-2 is-danger" @click="excluir(projeto.id)">
              <span class="ison is-small">
                <i class="fas fa-trash"></i>
              </span>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang="ts">
import { EXCLUIR_PROJETO } from "@/store/tipo-mmutacoes";
import { defineComponent, computed } from "vue";
import { useStore } from "../../store/index";

export default defineComponent({
  name: "ProjetosVue",
  methods: {
    excluir(id: string) {
      this.store.commit(EXCLUIR_PROJETO, id);
    },
  },
  setup() {
    const store = useStore();
    return {
      projetos: computed(() => store.state.projetos),
      store,
    };
  },
});
</script>