<template>
  <base-dialog v-if='inputIsInvalid' title='Invalid Input' @close='confirmError'>
    <template #default>
      <p>Unfortunately, one input value is invalid</p>
      <p>Please check all inputs and enter valid values.</p>
    </template>
    <template #actions>
      <base-button @click='confirmError'>Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent='submitData'>
      <div class='form-control'>
        <label for='title'>Title</label>
        <input id='title' ref='titleInput' name='title' type='text'>
      </div>
      <div class='form-control'>
        <label for='description'>Description</label>
        <textarea id='description' ref='descInput' name='description' rows='3'></textarea>
      </div>
      <div class='form-control'>
        <label for='Link'>Link</label>
        <input id='link' ref='linkInput' name='link' type='url'>
      </div>
      <div>
        <base-button type='submit'>Add Resource</base-button>
      </div>

    </form>
  </base-card>
</template>

<script>
import BaseCard from '@/components/UI/BaseCard';
import BaseButton from '@/components/UI/BaseButton';
import BaseDialog from '@/components/UI/BaseDialog';


export default {
  name: 'AddResource',
  components: {
    BaseDialog,
    BaseCard,
    BaseButton
  },
  data() {
    return {
      inputIsInvalid: false
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;
      if (enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === '') {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }

};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
