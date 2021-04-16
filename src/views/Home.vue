<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks"
import AddTask from "../components/AddTask"

export default {
  name: "Home",
  components: {
    Tasks,
    AddTask,
  },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [],
    }
  },
  methods: {
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id
          ? { ...task, reminder: (task.reminder = !task.reminder) }
          : task
      )
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
  },
  created() {
    this.tasks = [
      {
        id: "1",
        text: "Doctors Appointment",
        day: "March 5th at 2:30pm",
        reminder: true,
      },
      {
        id: "2",
        text: "Meeting with boss",
        day: "March 6th at 1:30pm",
        reminder: true,
      },
      {
        id: "3",
        text: "Food shopping",
        day: "March 7th at 2:00pm",
        reminder: false,
      },
    ]
  },
}
</script>
