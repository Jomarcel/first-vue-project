<template>
  <div class="container">
    <h1>My first Vue project</h1>
    <div v-if="showForm">
      <AddTask @add-task="addTask" />
    </div>
    <Header :showAddtask="toggleShow" title="Task tracker" />
    <Button
      @button-click="toggleShow"
      :text="showForm ? 'Close' : 'Show'"
      :color="showForm ? 'green' : 'red'"
    />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Button from "./components/Button";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
  name: "App",
  components: {
    Header,
    Button,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showForm: false,
    };
  },

  methods: {
    toggleShow() {
      this.showForm = !this.showForm;
    },
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      console.log("id", id);
      if (confirm("are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },

    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  created() {
    // console.log("hello");
    this.tasks = [
      {
        id: 1,
        text: "Doctors Appointment",
        day: "March 1st at 2:30",
        reminder: true,
      },
      {
        id: 2,
        text: "Some appointment",
        day: "Arpil 5th at 11:00-",
        reminder: false,
      },
      {
        id: 3,
        text: "Dentist Appointment",
        day: "January 9th at 9:30",
        reminder: true,
      },
    ];
  },
  // computed: {
  //   selectAll() {
  //     this.tasks.every((task) => {
  //       return task.reminder;
  //     });
  //   },
  // },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
