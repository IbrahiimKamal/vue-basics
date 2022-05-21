<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="invalid input"
    @close="confirmError"
  >
    <template #default>
      <p>Oops!, this is not invalid!</p>
      <p>Please check all Inputs</p>
    </template>
  </base-dialog>

  <form @submit.prevent="submitData">
    <div class="form-control">
      <label for="title">Title</label>
      <input type="text" name="title" id="title" ref="titleInput" />
    </div>
    <div class="form-control">
      <label for="description">Description</label>
      <textarea
        name="description"
        id="description"
        rows="3"
        ref="descInput"
      ></textarea>
    </div>
    <div class="form-control">
      <label for="link">Link</label>
      <input type="url" name="link" id="link" ref="linkInput" />
    </div>
    <div>
      <base-button type="submit">Add</base-button>
    </div>
  </form>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';

export default {
  inject: ['addResource'],

  data() {
    return {
      inputIsInvalid: false,
    };
  },

  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDesc = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDesc.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDesc, enteredLink);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },

  components: { BaseButton, BaseDialog },
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
