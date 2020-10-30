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
import _ from 'lodash';
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
