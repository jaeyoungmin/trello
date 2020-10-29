<template>
  <v-card class="list-box" elevation="3">
    <v-row class="box-header" align="center" no-gutters>
      <h2>{{ list.title }}</h2>
      <v-spacer></v-spacer>
      <v-btn icon><v-icon>mdi-dots-horizontal</v-icon></v-btn>
    </v-row>
    <div class="item-list-wrapper">
      <!-- <IssueCard v-for="(title, i) in filteredIssue" :key="i" :title="title" /> -->
      <issue-card
        v-for="(issue, i) in relatedIssues"
        :key="i"
        :issue="issue"
      ></issue-card>
    </div>
    <div class="btn-wrapper">
      <v-btn text color="#5e6c84">
        <v-icon>mdi-plus</v-icon>
        Add a card
      </v-btn>
    </div>
  </v-card>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'ListBox',
  components: {
    IssueCard: () => import('@/components/main/IssueCard.vue'),
  },
  props: ['list'],
  computed: {
    ...mapState(['issues']),
    relatedIssues() {
      return this.issues.filter((el) => el.listId === this.list.id);
    },
  },

  // props: ['lists', 'issues'],
  /* computed: {
    filteredIssue() {
      return this.issues.filter((el) => el.listId === this.lists.id);
    },
  },*/
};
</script>

<style lang="scss" scoped>
.list-box {
  margin: 30px;
  background-color: #ebecf0;
}
.box-header {
  padding: 5px 20px;
  h2 {
    font-size: 1.4rem;
  }
}
.btn-wrapper {
  padding: 5px;
}
.item-list-wrapper {
  padding: 5px;
}
</style>
