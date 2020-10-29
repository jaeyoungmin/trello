<template>
  <v-row class="main-view">
    <!-- <list-box
      v-for="(list, i) in lists"
      :key="i"
      class="list-box"
      :lists="list"
      :issues="issues"
    ></list-box> -->
    <list-box v-for="(list, i) in lists" :key="i" :list="list"></list-box>
  </v-row>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'Main',
  data() {
    return {
      abcd: '',
    };
  },
  components: {
    ListBox: () => import('@/components/main/ListBox.vue'),
  },
  computed: { ...mapState(['lists']) },

  // props: ['lists', 'issues'],
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
</style>
