<template>
  <div class="col-md-1">
    <div class="btn-group-vertical" role="group" aria-label="Button group with nested dropdown">
      <button type="button" class="btn btn-secondary" v-on:click="onSelected(item.tag)" v-bind:key="key" v-for="(item, key) in items">{{ item.text }}</button>
     </div>
  </div>
</template>

<script>
export default {
  name: "taksMenu",
  props: {
    items: Array
    },
  methods: {
    onSelected(tag) {
      this.$emit("click-select", tag);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
