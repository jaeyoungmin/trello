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
    <v-btn
      block
      elevation="0"
      color="#eaecef"
      class="action"
      @click="isDelete = true"
      ><v-icon style="margin-right:10px;">mdi-delete</v-icon>Delete
      <v-spacer></v-spacer
    ></v-btn>
    <v-fade-transition>
      <v-card class="delete-card" max-width="344" v-show="isDelete">
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="headline mb-1">
              Delete Card?
            </v-list-item-title>

            <v-divider></v-divider>
            <p>
              All actions will be removed from the activity feed and you won't
              be able to re-open. thire is no undo.
            </p>
          </v-list-item-content>
        </v-list-item>
        <v-card-actions>
          <v-btn color="red" dark min-width="150" @click="deleteIssue">
            Delete
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn icon @click="isDelete = false"
            ><v-icon>mdi-close</v-icon></v-btn
          >
        </v-card-actions>
      </v-card>
    </v-fade-transition>
  </div>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'actions',
  data() {
    return {
      isDelete: false,
    };
  },
  computed: {
    ...mapState(['lists']),
  },
  methods: {
    move(item) {
      this.$emit('move', item);
    },
    copy(item) {
      this.$emit('copy', item);
    },
    deleteIssue() {
      this.$emit('delete-issue');
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
.delete-card {
  p {
    font-size: 0.8rem;
    margin: 10px 0 0;
    color: gray;
  }
}
</style>
