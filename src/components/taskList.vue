<template>
  <div>
    <div>TaskList</div>
    <button class="changestate" @click="changeState">{{ nowstate }}</button>
    <div v-for="task in tasks" :key="task.name">
      <div class="task" v-if="isall && task.isExist">
        <button
          class="Fincheck"
          v-if="!task.isFinish"
          @click="finishTask(task)"
        >
          完
        </button>
        <div class="name">{{ task.name }}</div>
        <div class="date">{{ task.date }}まで</div>
        <button class="deleteTask" @click="deleteTask(task)">×</button>
      </div>
      <div class="task" v-if="!task.isFinish && !isall && task.isExist">
        <button class="Fincheck" @click="finishTask(task)">完</button>
        <div class="name">{{ task.name }}</div>
        <div class="date">{{ task.date }}まで</div>
        <button class="deleteTask" @click="deleteTask(task)">×</button>
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
      tasks: [
        { name: "やること１", date: "7/1", isFinish: false, isExist: true }
      ],
      newTodoName: "",
      newTodoDate: "",
      isall: false,
      nowstate: "現在：すべて表示"
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        name: this.newTodoName,
        date: this.newTodoDate,
        isFinish: false,
        isExist: true
      });
    },
    finishTask(task) {
      task.isFinish = true;
    },
    changeState() {
      if (!this.isall) {
        this.nowstate = "現在：未完のみ表示";
      } else {
        this.nowstate = "現在：すべて表示";
      }
      this.isall = !this.isall;
    },
    deleteTask(task) {
      task.isExist = false;
    }
  }
};
</script>

<style>
.task {
  display: flex;
  align-items: center;
  margin: 10px;
  border-bottom: gray 1px solid;
}
.Fincheck {
  width: 2em;
  height: 2em;
  margin-right: 10px;
}
.name {
  margin: 10px;
}
.date {
  margin: 10px;
}
</style>
