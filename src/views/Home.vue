<template>
  <div class="home">
    <core-app-bar></core-app-bar>
    <core-view></core-view>
    <!-- <core-view :lists="lists" :issues="issues"></core-view> -->
    <!-- <issue-detail
      v-for="(issue, i) in issues"
      :key="i"
      :issues="issue"
    ></issue-detail> -->
    <issue-detail></issue-detail>
  </div>
</template>

<script>
// @ is an alias to /src
// import { mapState } from 'vuex';
export default {
  name: 'Home',
  computed: {
    // ...mapState(['issues', 'lists']),
  },
  components: {
    CoreAppBar: () => import('@/components/core/AppBar.vue'),
    CoreView: () => import('@/components/core/View.vue'),
    IssueDetail: () => import('@/components/main/IssueDetail.vue'),
  },
};
</script>
<style lang="scss"></style>
