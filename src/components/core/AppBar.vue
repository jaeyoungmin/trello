<template>
  <v-app-bar flat solo color="white" height="60" class="app-bar">
    <v-btn depressed color="transparent"><v-icon>mdi-dots-grid</v-icon></v-btn>
    <v-btn depressed color="transparent"><v-icon>mdi-home</v-icon></v-btn>
    <v-btn depressed color="transparent"
      ><v-icon>mdi-trello</v-icon>Bords</v-btn
    >
    <v-text-field append-icon="mdi-magnify" solo flat class="text-field">
    </v-text-field>
    <v-spacer></v-spacer>
    <v-img
      max-width="100"
      src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSK2_JYw2lbbvo7c2dzgOfQCBMDewW7fGcJXw&usqp=CAU"
      alt="logo"
      class="logo"
    ></v-img>
    <v-spacer></v-spacer>
    <v-btn depressed color="transparent"><v-icon>mdi-plus</v-icon></v-btn>
    <v-btn depressed color="transparent"
      ><v-icon>mdi-alert-circle-outline</v-icon></v-btn
    >
    <v-btn depressed color="transparent"
      ><v-icon>mdi-bell-outline</v-icon></v-btn
    >
  </v-app-bar>
</template>

<script>
export default {
  name: 'AppBar',
};
</script>

<style lang="scss" scoped>
.text-field {
  position: relative;
  height: 40px;
  max-width: 130px;
}
</style>
