<template>
  <v-app>
    <v-main>
      <CrudOperations/>
    </v-main>
  </v-app>
</template>

<script>
import CrudOperations from './components/CrudOperations.vue';

export default {
  name: 'App',

  components: {
    CrudOperations
  },

  data: () => ({
    //
  }),
};
</script>
