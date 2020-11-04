<template>
  <v-row class="main-view">
    <list-box v-for="(list, i) in lists" :key="i" :list="list"></list-box>
    <v-btn
      elevation="0"
      width="300"
      class="ma-3"
      v-if="!isAddList"
      @click="isAddList = true"
      ><v-icon class="mr-1">mdi-plus</v-icon> Add another list
      <v-spacer></v-spacer
    ></v-btn>
    <v-card v-else class="add-list-box">
      <v-textarea
        v-model="newListTitle"
        placeholder="Enter a title for this card... "
        solo
        auto-grow
        hide-details
        class="mb-2 elevation-0"
        rows="2"
      ></v-textarea>
      <v-btn color="green" dark @click="addList">Add List</v-btn>
      <v-btn icon @click="isAddList = false"><v-icon>mdi-close</v-icon></v-btn>
    </v-card>
  </v-row>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'Main',
  data() {
    return {
      isAddList: false,
      newListTitle: '',
    };
  },
  methods: {
    addList() {
      this.$store.commit('addList', {
        id: this.newListId,
        title: this.newListTitle,
      });
      this.newListTitle = '';
    },
  },
  components: {
    ListBox: () => import('@/components/main/ListBox.vue'),
  },
  computed: {
    ...mapState(['lists']),
    newListtId() {
      return (
        this.lists.reduce((acc, cur) => {
          acc = Math.max(acc, cur.id);
          return acc;
        }, 0) + 1
      );
    },
  },
};
</script>

<style lang="scss" scoped>
.main-view {
  display: flex;
  flex-flow: row;
  overflow-x: auto;
  align-items: flex-start;
  height: calc(100vh - 60px);
}
.list-box {
  flex: 400px 0 0;
}
.add-list-box {
  margin: 10px;
  background-color: #ebecf0;
  min-width: 300px;
  padding: 10px;
}
</style>
