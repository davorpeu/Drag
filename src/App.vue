<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonRouterOutlet } from "@ionic/vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  data() {
    return {
      newBlock: "",
      arrBacklog: [
        { name: "Code SignUpPage" },
        { name: "Code SignUpPage" },
        { name: "Code SignUpPage" },
        { name: "Code SignUpPage" },
      ],
      arrInProgress: [],
      arrDone: [],
    };
  },
  methods: {
    add() {
      if (this.newBlock) {
        this.arrBacklog.push({ name: this.newBlock });
        this.newBlock = "";
      }
    },
  },
  components: {
    IonApp,
    IonRouterOutlet,
  },
});
</script>