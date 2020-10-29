<template>
  <div class="actions">
    <h4>Add to card</h4>
    <div class="card-wrapper">
      <v-btn block elevation="0" color="#eaecef" class="action"
        ><v-icon style="margin-right:10px;">mdi-account-outline</v-icon
        >Members<v-spacer></v-spacer
      ></v-btn>
      <v-btn block elevation="0" color="#eaecef" class="action"
        ><v-icon style="margin-right:10px;">mdi-tag-outline</v-icon
        >Labels<v-spacer></v-spacer
      ></v-btn>
      <v-btn block elevation="0" color="#eaecef" class="action"
        ><v-icon style="margin-right:10px;">mdi-clock-time-four-outline</v-icon
        >Due Date<v-spacer></v-spacer
      ></v-btn>
      <v-btn block elevation="0" color="#eaecef" class="action"
        ><v-icon style="margin-right:10px;">mdi-attachment</v-icon
        >Attachment<v-spacer></v-spacer
      ></v-btn>
      <v-btn block elevation="0" color="#eaecef" class="action"
        ><v-icon style="margin-right:10px;">mdi-credit-card-outline</v-icon
        >Cover<v-spacer></v-spacer
      ></v-btn>
      <!-- <v-text-field
        prepend-inner-icon="mdi-account-outline"
        solo-inverted
        dense
        flat
        placeholder="Members"
      ></v-text-field>
      <v-text-field
        prepend-inner-icon="mdi-tag-outline"
        solo-inverted
        dense
        flat
        placeholder="Labels"
      ></v-text-field>
      <v-text-field
        prepend-inner-icon="mdi-checkbox-marked-outline"
        solo-inverted
        dense
        flat
        placeholder="Checklist"
      ></v-text-field>
      <v-text-field
        prepend-inner-icon="mdi-clock-time-four-outline"
        solo-inverted
        dense
        flat
        placeholder="Due Date"
      ></v-text-field>
      <v-text-field
        prepend-inner-icon="mdi-attachment"
        solo-inverted
        dense
        flat
        placeholder="Attachment"
      ></v-text-field>
      <v-text-field
        prepend-inner-icon="mdi-credit-card-outline"
        solo-inverted
        dense
        flat
        placeholder="Cover"
      ></v-text-field> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'Actions',
};
</script>

<style lang="scss" scoped>
.actions {
  padding: 10px;
}
.action {
  margin: 10px 0;
}
</style>
