<template>
  <div class="check-list">
    <v-row align="center" no-gutters>
      <v-icon>mdi-checkbox-marked-outline</v-icon>
      <h4 class="header-left-margin">Checklist</h4>
      <v-spacer></v-spacer>
      <v-btn small elevation="1" class="header-left-margin">Delete</v-btn>
    </v-row>
    <v-row align="center" no-gutters class="progress-wrapper">
      <span style="margin-right:10px; font-size:12px;"
        >{{ Math.round(progress) }}%</span
      >
      <v-col>
        <v-progress-linear
          rounded
          :value="progress"
          color="red darken-2"
          height="6"
        ></v-progress-linear>
      </v-col>
    </v-row>
    <div class="checkbox-list-wrapper">
      <v-checkbox
        v-for="(task, i) in tasks"
        :key="i"
        v-model="task.complete"
        label="task.title"
        class="check-list-item"
      ></v-checkbox>
    </div>
    <div class="buttons-wrapper">
      <v-btn style="margin-left:35px" elevation="0" small>Add an item</v-btn>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CheckList',
  props: ['tasks'],
  data() {
    return {
      // tasks: [
      //   { title: 'task1', complete: true },
      //   { title: 'task2', complete: false },
      //   { title: 'task3', complete: false },
      // ],
    };
  },
  computed: {
    progress() {
      let completeNum = this.tasks.filter((el) => el.complete).length;
      return (completeNum / this.tasks.length) * 100;
    },
  },
};
</script>

<style lang="scss" scoped>
.check-list {
  padding: 10px 0;
}
.header-left-margin {
  margin-left: 15px;
}
.progress-wrapper {
  margin: 10px 0;
}
.check-list-item {
  margin: 5px 0;
  height: 40px;
}
</style>
