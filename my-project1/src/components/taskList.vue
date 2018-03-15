<template>
  <div class="col-md-6">
    <div class="list-group">
      <task-item v-bind:item="item" v-on:click-complete="onCompleted" :key="key" v-bind:tag="tag" v-for="(item, key) in items"></task-item>
    </div>
  </div>
</template>

<script>
import taskItem from "./taskItem.vue";

export default {
  name: "taskList",
  components: {
    taskItem
  },
  props: {
    items: Array,
    tag: Boolean
  },
  methods: {
    onCompleted(id) {
      this.$emit("click-complete", id);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
