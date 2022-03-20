<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="closeDialog">
    <template #body>
      <p>Unfortunately one or more of your Inputs are empty!</p>
    </template>
    <template #actions>
      <base-button @click="closeDialog">OK</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitResource">
      <div class="form-control">
        <label for="name">Title: </label>
        <input type="text" name="name" id="name" ref="title" />
      </div>
      <div class="form-control">
        <label for="description">Description: </label>
        <textarea
          type="text"
          name="description"
          id="description"
          rows="3"
          ref="description"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link: </label>
        <input type="url" name="link" id="link" ref="link" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../ui/BaseButton.vue';
import BaseCard from '../ui/BaseCard.vue';
import BaseDialog from '../ui/BaseDialog.vue';

export default {
  components: { BaseCard, BaseButton, BaseDialog },
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submitResource() {
      const resourceID = new Date().toISOString();
      const inputTitle = this.$refs.title.value;
      const inputDescription = this.$refs.description.value;
      const inputLink = this.$refs.link.value;
      if (
        inputTitle.trim() === '' ||
        inputDescription.trim() === '' ||
        inputLink.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.pushResource(resourceID, inputTitle, inputDescription, inputLink);
    },
    closeDialog() {
      this.inputIsInvalid = false;
    },
  },
  inject: ['pushResource'],
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
