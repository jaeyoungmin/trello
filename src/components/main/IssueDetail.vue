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
            <DueDate
              :init-date="currentIssue.dueDate"
              @change-date="changeDate"
            />
            <!-- @change -date 커스텀 이벤트 발생  -->
            <Description
              :init-descr="currentIssue.description"
              @change-descr="changeDescr"
            />
            <CheckList
              :tasks="currentIssue.checklist"
              @add-check-item="addCheckListItem"
            />
            <Activity
              :activities="currentIssue.activities"
              @add-comment="addComment"
              @edit-comment="editComment"
              @delete-comment="deleteComment"
            />
          </v-col>
          <v-col cols="4" class="right-side">
            <Action />
            <Actions
              @move="moveToList"
              @copy="copyToList"
              @delete-issue="deleteIssue"
            />
          </v-col>
        </v-row>
      </v-card>
    </div>
  </v-overlay>
</template>

<script>
import { mapState } from 'vuex';
import _ from 'lodash';
export default {
  name: 'IssueDetail',
  data() {
    return {};
  },
  props: ['lists'],
  computed: {
    ...mapState(['isDetailShow', 'currentIssue', 'issues']),
    newIssueId() {
      return (
        this.issues.reduce((acc, cur) => {
          acc = Math.max(acc, cur.id);
          return acc;
        }, 0) + 1
      );
    },
  },
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
    changeDate(date) {
      // console.log('change date:', date);
      this.$store.commit('fixDate', {
        id: this.currentIssue.id,
        dueDate: date,
      });
    },
    changeDescr(text) {
      // console.log('chage description :', text);
      // this.$store.commit('fixDescr', {
      //   id: this.currentIssue.id,
      //   descr: text,
      // });
      let clone = _.cloneDeep(this.currentIssue);
      clone.description = text;
      this.$store.commit('editIssue', clone);
    },
    //npm install lodash 사용
    addCheckListItem(item) {
      let clone = _.cloneDeep(this.currentIssue);
      clone.checklist.push(item);
      this.$store.commit('editIssue', clone);
    },
    addComment(comment) {
      let clone = _.cloneDeep(this.currentIssue);
      clone.activities.push(comment);
      this.$store.commit('editIssue', clone);
    },
    editComment(comment) {
      let clone = _.cloneDeep(this.currentIssue);
      let target = clone.activities.find((el) => el.id === comment.id);
      target.text = comment.text;
      this.$store.commit('editIssue', clone);
    },
    deleteComment(id) {
      let clone = _.cloneDeep(this.currentIssue);
      let targetIndex = clone.activities.findIndex((el) => el.id === id);
      clone.activities.splice(targetIndex, 1);
      this.$store.commit('editIssue', clone);
    },
    moveToList(item) {
      let clone = _.cloneDeep(this.currentIssue);
      clone.listId = item.id;
      this.$store.commit('editIssue', clone);
    },
    copyToList(item) {
      let clone = _.cloneDeep(this.currentIssue);
      // clone.id = this.newIssueId;
      clone.listId = item.id;
      this.$store.commit('addIssue', clone);
    },
    deleteIssue() {
      this.$store.commit('deleteIssue', this.currentIssue.id);
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
