<template>
  <div class="description">
    <v-row class="description-header" align="center" no-gutters>
      <v-icon>mdi-text-subject</v-icon>
      <h4 class="header-left-margin">Description</h4>
      <v-btn elevation="1" small>Edit</v-btn>
    </v-row>
    <div>
      <p>{{ descr }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'description',
  props: ['descr'],
};
</script>

<style lang="scss" scoped>
.description {
  margin: 10px 0;
  p {
    margin: 10px 35px;
  }
}
.header-left-margin {
  margin: 0 15px;
}
</style>
