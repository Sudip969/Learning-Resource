<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError" >
    <template #default>
      <p>Unfortunately,At Least One Input Value is Invalid</p>
      <p>Please Check All Inputs</p>
    </template>
    <template #actions>
        <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          row="3"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Title</label>
        <input type="url" id="link" name="link" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  inject: ["addResource"],
  methods: {
    onSubmit() {
      const eTitle = this.$refs.titleInput.value;
      const eDesc = this.$refs.descInput.value;
      const eLink = this.$refs.linkInput.value;
      if (eTitle.trim() === "" || eDesc.trim() === "" || eLink.trim() === "") {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(eTitle, eDesc, eLink);
    },
    confirmError(){
        this.inputIsInvalid=false;
    }
  },
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
