<template>
  <v-overlay :value="isDetailShow">
    <div class="scroll-view">
      <v-card class="issue-detail-card" light elevation="10">
        <div class="issue-detail-header">
          <v-icon>mdi-inbox-full</v-icon>
          <h2>{{ currentIssue.title }}</h2>
          <p>In list {{ 'todo' }}</p>
          <v-btn icon class="close-btn" @click="closeDetail"
            ><v-icon>mdi-close</v-icon></v-btn
          >
        </div>
        <v-row>
          <v-col cols="8" class="left-side">
            <DueDate :date="currentIssue.dueDate" />
            <Description :descr="currentIssue.description" />
            <CheckList :tasks="currentIssue.checklist" />
            <Activity :activities="currentIssue.activities" />
          </v-col>
          <v-col cols="4" class="right-side">
            <Action />
            <Actions />
          </v-col>
        </v-row>
      </v-card>
    </div>
  </v-overlay>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'IssueDetail',
  data() {
    return {};
  },
  props: ['issues'],
  computed: { ...mapState(['isDetailShow', 'currentIssue']) },
  components: {
    DueDate: () => import('@/components/issue_detail/DueDate.vue'),
    Description: () => import('@/components/issue_detail/Description.vue'),
    CheckList: () => import('@/components/issue_detail/CheckList.vue'),
    Activity: () => import('@/components/issue_detail/Activity.vue'),
    Action: () => import('@/components/issue_detail/Action.vue'),
    Actions: () => import('@/components/issue_detail/Actions.vue'),
  },
  methods: {
    closeDetail() {
      this.$store.commit('toggleIsDetailShow');
    },
  },
};
</script>

<style lang="scss" scoped>
.scroll-view {
  max-height: 80vh;
  overflow-y: auto;
}
.issue-detail-card {
  max-width: 800px;
  width: 100vw;
  min-height: 80vh;
  padding: 20px;
  background-color: #f4f5f7;
}
.issue-detail-header {
  position: relative;
  h2 {
    display: inline-block;
    margin: 0 0 0 10px;
  }
  p {
    font-size: 14px;
    margin: 0 0 0 35px;
  }
  .close-btn {
    position: absolute;
    top: 0;
    right: 0;
  }
}
</style>
