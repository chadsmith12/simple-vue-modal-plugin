<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <input type="text" v-model="id" />
    <button type="button" @click="openModal">Open Modal</button>

    <UserForm :id="id" v-model="isModalOpen"></UserForm>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import AppModal from "@/components/modal/AppModal.vue";
import UserForm from "@/components/UserForm.vue";

@Component({
  components: {
    HelloWorld,
    AppModal,
    UserForm
  }
})
export default class Home extends Vue {
  private isModalOpen: boolean = false;

  private id: string = '';

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
