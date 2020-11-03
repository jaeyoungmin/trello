<template>
  <div class="activity">
    <v-row class="activity-header" align="center" no-gutters>
      <v-icon>mdi-timeline-text-outline</v-icon>
      <h4 class="header-left-margin">Activity</h4>
    </v-row>
    <v-row class="comment-text-field-wrapper" align="center" no-gutters>
      <v-avatar><v-img :src="profileImg"></v-img></v-avatar>
      <v-text-field
        outlined
        solo
        flat
        v-model="newComment"
        placeholder="Write a comments..."
        class="comment-text-field"
        @keyup.enter="save"
      >
        <template v-slot:append
          ><v-btn color="green" text small @click="save">save</v-btn></template
        >
      </v-text-field>
    </v-row>
    <div class="activity-list-wrapper">
      <v-row no-gutters v-for="(comment, i) in orderedActivities" :key="i">
        <div class="profile-wrapper">
          <v-avatar><v-img :src="comment.imgSrc"></v-img></v-avatar>
        </div>
        <div class="text-wrapper">
          <p>
            <strong>{{ comment.name }}</strong
            ><span class="date-text">{{ formatDate(comment.createdAt) }}</span>
          </p>
          <v-card class="text-card">
            <p v-if="!(isEdit === i)">{{ comment.text }}</p>
            <div v-else>
              <v-textarea
                solo
                flat
                auto-grow
                v-model="editedComment"
                row-height="15"
                rows="2"
              ></v-textarea>
              <v-btn
                x-small
                color="green"
                dark
                elevation="0"
                @click="edit(comment.id)"
                >save</v-btn
              >
              <v-btn icon x-small @click="isEdit = undefined"
                ><v-icon>mdi-close</v-icon></v-btn
              >
            </div>
          </v-card>
          <div class="activity-actions">
            <!-- <button @click="isEdit = i">Edit</button> -->
            <button @click="toEdit(comment.text, i)">Edit</button>
            <button @click="deleteComment(comment.id)">Delete</button>
          </div>
          <!-- <v-text-field
              class="comment-input mb-2"
              v-model="comment.text"
              :readonly="isEdit !== i"
              :dark="isEdit === i"
              solo
              hide-details
            ></v-text-field>
          </div>
          <div class="activity-actions">
            <button class="mr-2" @click="isEdit = i">Edit</button>
            <button>Delete</button>
          </div> -->
        </div>
      </v-row>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import moment from 'moment';
export default {
  name: 'Activity',
  props: ['activities'],
  data() {
    return {
      newComment: '',
      isEdit: undefined,
      editedComment: '',
      profileImg:
        'https://jmagazine.joins.com/_data/photo/2019/04/2949993301_QGcF14Px_1.jpg',
      // activities: [
      //   {
      //     id: 0,
      //     imgSrc: 'https://pbs.twimg.com/media/D0AEcLJVYAErhXl.jpg',
      //     name: 'nickname',
      //     text: 'Hi my name is IU',
      //     createdAt: '2020-10-27T08:09:34.345Z',
      //   },
      //   {
      //     id: 0,
      //     imgSrc: 'https://pbs.twimg.com/media/D0AEcLJVYAErhXl.jpg',
      //     name: 'Name',
      //     text: 'Hi my name is iu',
      //     createdAt: '2020-10-24T03:09:34.345Z',
      //   },
      // ],
    };
  },
  computed: {
    newCommentId() {
      return (
        this.activities.reduce((acc, cur) => {
          acc = Math.max(acc, cur.id);
          return acc;
        }, 0) + 1
      );
    },
    orderedActivities() {
      let clone = _.cloneDeep(this.activities);
      return clone.sort(
        (a, b) => moment(b.createdAt).unix() - moment(a.createdAt).unix()
      );
    },
  },
  methods: {
    toEdit(comment, index) {
      this.isEdit = index;
      this.editedComment = comment;
    },
    formatDate(date) {
      let created = moment(date);
      //console.log(created.format('dddd, MMM, Do'));
      // console.log(moment().utc().format()); utc시간으로 변환
      //console.log(moment().valueOf()); uixMillisecond시간으로 변환
      return created.format('dddd. MMM. Do. [at] HH:mm a');
      // return created.format('dddd. MMM. Do.  h:mm a');
    },
    edit(id) {
      this.$emit('edit-comment', { text: this.editedComment, id: id });
      this.isEdit = undefined;
    },
    save() {
      this.$emit('add-comment', {
        id: this.newCommentId,
        imgSrc: this.profileImg,
        name: 'WOW',
        text: this.newComment,
        createdAt: moment().toISOString(),
      });
      this.newComment = '';
    },
    deleteComment(id) {
      this.$emit('delete-comment', id);
    },
  },
};
</script>

<style lang="scss" scoped>
.header-left-margin {
  margin-left: 15px;
}
.comment-text-field-wrapper {
  margin: 10px 0;
}
.comment-text-field {
  height: 56px;
  margin-left: 10px;
}

.text-wrapper {
  margin-left: 11px;
}
.date-text {
  margin-left: 10px;
  color: gray;
  font-size: 13px;
}
.text-card {
  display: inline-block;
  padding: 10px;
  p {
    margin: 0;
  }
}
.activity-actions {
  button {
    margin-right: 10px;
    font-size: 13px;
    text-decoration-line: underline;
  }
}
.edit-form {
  margin: 10px 0 0;
  padding: 0;
}
</style>
