<template>
  <div>
    <h1 class="mb-4">Dogs for Adoption</h1>
    <b-table striped hover :items="dogs">
      <template v-slot:cell(name)="data">
        <router-link :to="`/pets/dogs/${data.index}`">{{
          data.value
        }}</router-link>
      </template>
    </b-table>
  </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  data () {
    return {}
  },
  computed: {
    ...mapState(['dogs'])
  }
}
</script>
