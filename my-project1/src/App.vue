<template>
  <div id="app" class="container">
    <div class="row justify-content-md-center mt-5">
      <task-menu v-on:click-select="onSelected" v-bind:items="menus"></task-menu>
      <task-list v-bind:tag="currentMenuStatus" v-on:click-complete="onCompleted" v-bind:items="tasks"></task-list>
    </div>
  </div>
</template>

<script>
import taskMenu from "./components/taskMenu.vue";
import taskItem from "./components/taskItem.vue";
import taskList from "./components/taskList.vue";
import axios from "axios";
import * as R from "ramda";

export default {
  name: "app",
  components: {
    taskMenu,
    taskItem,
    taskList
  },
  data() {
    return {
      menus: [
        {
          tag: false,
          text: "未完成"
        },
        {
          tag: true,
          text: "完成"
        }
      ],
      currentMenuStatus: false,
      tasks: [] // [{id, title, content, completed, createAt, completeAt }]
    };
  },
  beforeCreate() {
    axios
      .get("https://api.myjson.com/bins/d9yjl")
      .then(response => response.data)
      .then(data => (this.tasks = data))
      .catch(console.log);
  },
  methods: {
    onSelected(tag) {
      this.currentMenuStatus = tag;
    },
    onCompleted(id) {
      var index = R.findIndex(R.propEq("id", id))(this.tasks);
      this.tasks[index].completed = true;
      this.save();
    },
    save() {
      axios
        .put("https://api.myjson.com/bins/d9yjl", this.tasks)
        .then(response => response.data)
        .then(() => alert("更新成功"))
        .catch(console.log);
    }
  }
};
</script>

<style>

</style>
