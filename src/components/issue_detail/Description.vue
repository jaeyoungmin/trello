<template>
  <div class="description">
    <v-row class="description-header" align="center" no-gutters>
      <v-icon>mdi-text-subject</v-icon>
      <h4 class="header-left-margin">Description</h4>
      <v-btn v-if="!isEdit" elevation="1" small @click="isEdit = true"
        >Edit</v-btn
      >
    </v-row>
    <div>
      <p v-if="!isEdit">{{ descr }}</p>
      <div class="edit-form" v-else>
        <v-textarea v-model="descr" solo auto-grow rows="1"></v-textarea>
        <v-btn small color="green" dark @click="save">Save</v-btn>
        <v-btn small icon @click="(isEdit = false), (descr = initDescr)"
          ><v-icon>mdi-close</v-icon></v-btn
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Description',
  props: ['initDescr'],
  data() {
    return {
      isEdit: false,
      descr: this.initDescr,
      newTask: '',
    };
  },
  methods: {
    save() {
      this.$emit('change-descr', this.descr);
      this.isEdit = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.description {
  margin: 10px 0;
  p {
    margin: 0 35px;
  }
}
.header-left-margin {
  margin: 0 15px;
}
.edit-form {
  margin: 10px 37px;
}
</style>
