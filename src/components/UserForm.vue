<template>
<AppModal 
    :title="title" 
    :value="value" 
    @visibility-change="onVisibleChange"
    @save="save">
    <input type="text" v-model="username" />
    <input type="text" v-model="firstName" />
</AppModal>
</template>


<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import AppModal from "@/components/modal/AppModal.vue";

const components = {AppModal};

@Component({
    components: components
})
export default class UserForm extends Vue {
    @Prop() private id!: number;
    @Prop() private value!: boolean;

    private username: string = '';
    private firstName: string = '';

    private get title(): string {
        return `Editing User ${this.id}`;
    }

    private onVisibleChange(newVal: boolean): void {
        if(!newVal) {
            this.$emit('input', newVal);
        }
        else  {
            setTimeout(() => {
                this.username = 'Chad';
                this.firstName = 'smith'
            }, 100);
        }
    }

    private save(): void {
        this.$emit('save-success');
        this.$emit('input', false);
        this.resetFields();
    }

    private resetFields(): void{
        this.username = '';
        this.firstName = '';
    }
}
</script>