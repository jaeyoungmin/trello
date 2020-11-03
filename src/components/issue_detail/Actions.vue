<template>
  <div class="actions">
    <h4>Action</h4>
    <v-menu offset-y>
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          block
          elevation="0"
          color="#eaecef"
          class="action"
          v-bind="attrs"
          v-on="on"
          ><v-icon style="margin-right:10px;">mdi-arrow-right</v-icon>Move
          <v-spacer></v-spacer
        ></v-btn>
      </template>
      <v-list>
        <v-list-item v-for="(item, i) in lists" :key="i">
          <v-list-item-title @click="move(item)">{{
            item.title
          }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <v-menu offset-y>
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          block
          elevation="0"
          color="#eaecef"
          class="action"
          v-bind="attrs"
          v-on="on"
          ><v-icon style="margin-right:10px;">mdi-content-copy</v-icon>Copy
          <v-spacer></v-spacer
        ></v-btn>
      </template>
      <v-list>
        <v-list-item v-for="(item, i) in lists" :key="i">
          <v-list-item-title @click="copy(item)">{{
            item.title
          }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>

    <v-btn block elevation="0" color="#eaecef" class="action"
      ><v-icon style="margin-right:10px;">mdi-delete</v-icon>Delete
      <v-spacer></v-spacer
    ></v-btn>
  </div>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'actions',
  computed: { ...mapState(['lists', 'issues']) },
  methods: {
    move(item) {
      this.$emit('move', item);
    },
    copy(item) {
      this.$emit('copy', item);
    },
  },
};
</script>

<style lang="scss" scoped>
.actions {
  padding: 10px;
}
.action {
  margin: 10px 0;
}
</style>
