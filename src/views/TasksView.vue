<template>
  <div>
    <h1>Задачи</h1>

    <form class="form">
      <input class="from__input" v-model="formValue" type="text" placeholder="Введите задачу">

      <button @click.prevent="addTask(formValue)" class="from__btn btn">Добавить</button>
    </form>

    <div class="list">
      <TaskItem
        v-for="task of taskList"
        :key="task.id"
        :id="task.id"
        :value="task.body"
        :removeTask="removeTask"
        :editTask="editTask"
      />

      <p v-show="taskList.length < 1">Тут пока пусто...</p>
    </div>

  </div>
</template>

<script>
import TaskItem from '../components/TaskItem.vue';

export default {
  components: {TaskItem},
  data() {
    return {
        formValue: '',
        taskList: []
    };
  },
  methods: {
    getTasks(){
        if (localStorage.getItem('tasks') === null) {
            localStorage.setItem('tasks', JSON.stringify([]))
        }
        return JSON.parse(localStorage.getItem('tasks'))
    },
    getId(){
        let list = this.getTasks();
        let max = list.reduce((i, a) => i.id > a.id ? i : a, 0);

        return max === 0 ? 0 : max.id + 1;
    },
    addTask(val){
      if (this.formValue === '') return
      
      this.taskList.push({'id': this.getId(),'body': val});
      
      localStorage.setItem('tasks', JSON.stringify(this.taskList))
      this.formValue = '';
    },
    editTask(oldValue, newValue){
      this.taskList.find(t => t.body === oldValue).body = newValue;
      localStorage.setItem('tasks', JSON.stringify(this.taskList))
    },
    removeTask(id){
      this.taskList = this.taskList.filter(t => t.id !== id)
      localStorage.setItem('tasks', JSON.stringify(this.taskList))
    }
  },
  created(){
    //localStorage.clear()
    if (!localStorage.hasOwnProperty("tasks")) {
      localStorage.setItem('tasks', JSON.stringify([]))
    }
    this.taskList = JSON.parse(localStorage.getItem('tasks'))
  }
}

</script>

<style scoped>
.form {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.from__input {
  padding: 10px;
  width: 300px;
  height: 45px;
  border-radius: 5px;
}

.list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
