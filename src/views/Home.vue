<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <button type="button" @click="openModal">Open Modal</button>
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />

    <AppModal
      title="Hello  World"
      v-model="isModalOpen"
      :stay-open="true"
      @save="saveForm"
    >
      This is the default modal!
    </AppModal>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import AppModal from "@/components/modal/AppModal.vue";

@Component({
  components: {
    HelloWorld,
    AppModal
  }
})
export default class Home extends Vue {
  private isModalOpen: boolean = false;

  private openModal() {
    this.isModalOpen = true;
  }
  private saveForm() {
    setTimeout(() => {
      this.isModalOpen = false;
    }, 2000);
  }
}
</script>
