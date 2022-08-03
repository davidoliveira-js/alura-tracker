<template>
  <BoxComponent>
    <div class="collums">
      <div class="collumn is-7">
        {{ tarefa.descricao || "Tarefa sem descrição" }}
      </div>
      <div class="collumn">
        <CronometroComponent :tempoEmSegundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </BoxComponent>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import CronometroComponent from "./Cronometro.vue";
import ITarefa from "../interfaces/ITarefa";
import BoxComponent from "./Box.vue";

export default defineComponent({
  name: "TarefaComponent",
  components: {
    CronometroComponent,
    BoxComponent,
  },
  props: {
    tarefa: {
      type: Object as PropType<ITarefa>,
      required: true,
    },
  },
});
</script>
