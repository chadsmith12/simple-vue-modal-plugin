<template>
  <div class="app-modal-backdrop" v-show="isVisible">
    <div class="app-modal">
      <header class="app-modal-header">
        <slot name="header">
          {{ title }}
          <button type="button" class="btn-close" @click="close">x</button>
        </slot>
      </header>

      <slot></slot>

      <footer class="app-modal-footer">
        <slot name="footer">
          <button type="button" class="btn-green" @click="save">Save</button>
        </slot>
      </footer>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit, Watch } from "vue-property-decorator";

@Component({})
export default class AppModal extends Vue {
  @Prop() private value!: boolean;
  @Prop() private stayOpen!: boolean;
  @Prop() private title!: string;

  private isVisible: boolean = this.value;
  
  @Watch("value")
  private onValueChange(newVal: boolean) {
    this.isVisible = newVal;
    this.emitVisibilityChange(newVal);
  }

  @Emit()
  private close(): boolean {
    this.$emit("close");
    this.isVisible = false;
    this.emitInput(false);
    this.emitVisibilityChange(false);
    return false;
  }

  private save(): void {
    // go ahead and emit the save event.
    // if we are supposed to stay open then go ahead and return.
    // user will handle closing the modal automatically.
    this.$emit("save");
    if (this.stayOpen) {
    return;
    }

    this.isVisible = false;
    this.emitInput(false);
    this.emitVisibilityChange(false);
  }

  private emitVisibilityChange(value: boolean): void {
    this.$emit("visibility-change", value);
  }

  private emitInput(value: boolean): void {
    this.$emit("input", value);
  }
}
</script>

<style scoped>
.app-modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.app-modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.app-modal-header .app-modal-footer {
  padding: 15px;
  display: flex;
}

.app-modal-header {
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.app-modal-footer {
  border-top: #eeeeee;
  justify-content: flex-end;
}

.app-modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  border: none;
  font-size: 20px;
  padding: 20px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
</style>
