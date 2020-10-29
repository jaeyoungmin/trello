<template>
  <div class="due-date-section">
    <h5>DUE DATE</h5>
    <v-menu
      v-model="menu"
      :close-on-content-click="false"
      transition="scale-transition"
      offset-y
      min-width="290px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-row class="check-box d-flex align-center" no-gutters>
          <v-checkbox></v-checkbox>
          <v-btn class="date-btn" small v-bind="attrs" v-on="on" elevation="1"
            >{{ date }}{{ time }}</v-btn
          >
        </v-row>
      </template>
      <v-date-picker v-model="date" @input="menu = false"></v-date-picker>
    </v-menu>
  </div>
</template>

<script>
export default {
  name: 'DueDate',
  props: ['date'],
  data: () => ({
    // date: new Date().toISOString().substr(0, 10),
    // time: new Date().toLocaleTimeString().substr(2, 5),
    menu: false,
  }),
};
</script>

<style lang="scss" scoped>
.due-date-section {
  padding: 0 35px;
  .check-box {
    margin-top: -10px;
    margin-left: 1px;
  }
}
</style>
