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
          <v-btn
            class="date-btn"
            small
            v-bind="attrs"
            v-on="on"
            elevation="1"
            >{{ date }}</v-btn
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
  props: ['initDate'],
  data() {
    return {
      menu: false,
      date: this.initDate,
    };
  },
  watch: {
    date(newValue) {
      this.$emit('change-date', newValue);
    },
  },
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
