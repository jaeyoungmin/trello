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
      <v-btn
        small
        text
        color="#5e6c84"
        v-if="!isAddCard"
        @click="isAddCard = true"
      >
        <v-icon>mdi-plus</v-icon>
        Add another card
      </v-btn>
      <div v-else>
        <v-textarea
          v-model="newCardTitle"
          placeholder="Enter a title for this card... "
          solo
          auto-grow
          hide-details
          class="mb-2 elevation-0"
          rows="2"
        ></v-textarea>
        <v-btn color="green" dark @click="addCard">Add Card</v-btn>
        <v-btn icon @click="isAddCard = false"
          ><v-icon>mdi-close</v-icon></v-btn
        >
      </div>
    </div>
  </v-card>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'ListBox',
  data() {
    return {
      newCardTitle: '',
      isAddCard: false,
    };
  },
  components: {
    IssueCard: () => import('@/components/main/IssueCard.vue'),
  },
  props: ['list'],
  computed: {
    ...mapState(['issues']),
    relatedIssues() {
      return this.issues.filter((el) => el.listId === this.list.id);
    },
    newIssueId() {
      return (
        this.issues.reduce((acc, cur) => {
          acc = Math.max(acc, cur.id);
          return acc;
        }, 0) + 1
      );
    },
  },
  methods: {
    addCard() {
      let defaultIssueForm = {
        id: this.newIssueId,
        listId: this.list.id,
        title: this.newCardTitle,
        description: '',
        dueDate: '',
        checklist: [],
        activities: [],
      };
      this.$store.commit('addIssue', defaultIssueForm);
      this.newCardTitle = '';
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
  margin: 10px;
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
.title-wrapper {
  margin: -5px 0px 10px;
}
.title-btn {
  margin: 5px 0;
}
</style>
