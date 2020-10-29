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
        v-model="newText"
        placeholder="Write a comments..."
        class="comment-text-field"
        @keyup.enter="addComment"
      >
      </v-text-field>
    </v-row>
    <div class="activity-list-wrapper">
      <v-row no-gutters v-for="(comment, i) in activities" :key="i">
        <div class="profile-wrapper">
          <v-avatar><v-img :src="comment.imgSrc"></v-img></v-avatar>
        </div>
        <div class="text-wrapper">
          <p>
            <strong>{{ comment.name }}</strong
            ><span class="date-text">{{ formatDate(comment.createdAt) }}</span>
          </p>
          <v-card class="text-card">
            <p>{{ comment.text }}</p>
          </v-card>
          <div class="activity-actions">
            <button>Edit</button>
            <button>Delete</button>
          </div>
        </div>
      </v-row>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
export default {
  name: 'Activity',
  props: ['activities'],
  data() {
    return {
      newText: '',
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

  methods: {
    formatDate(date) {
      let created = moment(date);
      //console.log(created.format('dddd, MMM, Do'));
      // console.log(moment().utc().format()); utc시간으로 변환
      //console.log(moment().valueOf()); uixMillisecond시간으로 변환
      return created.format('dddd, MMM, Do');
    },
    addComment() {
      this.$store.commit('addComment', {
        id: 0,
        imgSrc: 'https://pbs.twimg.com/media/D0AEcLJVYAErhXl.jpg',
        name: 'Name',
        text: this.newText,
        createdAt: '2020-10-24T03:09:34.345Z',
      });
      this.newText = '';
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
</style>
