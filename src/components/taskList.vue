<template>
  <div>
    <div>TaskList</div>
    <div v-for="task in tasks" :key="task.name">
      <div class="task" v-if="!task.isFinish">
        <button class="Fincheck" @click="finishTask(task)">完了</button>
        <div class="name">{{ task.name }}</div>
        <div class="date">{{ task.date }}まで</div>
      </div>
    </div>
    <div>
      <label>
        タスク内容
        <input type="text" v-model="newTodoName" />
      </label>
      <label>
        期日
        <input type="text" v-model="newTodoDate" />
      </label>
      <button @click="addTask">add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "taskList",
  data() {
    return {
      tasks: [{ name: "やること１", date: "7/1", isFinish: false }],
      newTodoName: "",
      newTodoDate: ""
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        name: this.newTodoName,
        date: this.newTodoDate,
        isFinish: false
      });
    },
    finishTask(task) {
      task.isFinish = true;
    }
  }
};
</script>