<template>
  <div class="home">
    <h1>Adopt a new best friend</h1>
    <p>No. of Cats: {{ getAllCats.length }}</p>
    <p>No. of Dogs: {{ getAllDogs.length }}</p>
    <p>Total Animals Count: {{ animalsCount }}</p>
    <button @click="togglePetForm" class="btn btn-outline-secondary">Add New Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm" class="my-5">
      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
        <b-form-input id="input-2" type="text" v-model="formData.name" required placeholder="Enter name"></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select id="input-3" v-model="formData.species" :options="['cats', 'dogs']" required></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
        <b-form-input id="input-2" type="number" v-model="formData.age" required placeholder="Enter age"></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger" class="ml-3">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
export default {
  name: 'home',
  data() {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null,
      },
    };
  },
  computed: {
    ...mapGetters(['animalsCount', 'getAllCats', 'getAllDogs']),
  },
  methods: {
    ...mapActions(['addPet']),
    togglePetForm() {
      this.showPetForm = !this.showPetForm;
    },
    handleSubmit() {
      const { species, age, name } = this.formData;
      const payload = {
        species,
        pet: {
          name,
          age,
        },
      };
      this.addPet(payload);
      // reset the form after submtting

      this.formData = {
        name: '',
        age: 0,
        species: null,
      };
    },
  },
};
</script>
