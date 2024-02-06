<script>
import assignment from './data/assignment.json';

let id = 0;

export default {
  // Properties returned from data() become reactive state
  // and will be exposed on `this`.
  data() {
    return {
      assignment: assignment,
      hideCompleted: false,
    };
  },

  // Computed Properties are automatically updated when dependencies change
  computed: {
    filteredTasks() {
      // These results will be cached until the dependencies change.
      return this.hideCompleted
        ? this.assignment.filter((t) => !t.status)
        : this.assignment;
    },
    daysRemainings() {
    return dueDate => {
      const now = new Date();
      const due = new Date(dueDate);
      const timeDiff = due.getTime() - now.getTime();
      const daysRemaining = Math.ceil(timeDiff / (1000 * 3600 * 24));
      return daysRemaining;
    };
  }
  },

  

  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event listeners in templates.
  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {
    this.assignment= assignment;
  },

  
};


</script>

<template>


  <h2>Task List</h2>
  <ul>
    <li v-for="assignment in filteredTasks" :key="assignment.id">
      <span :class="{ done: assignment.status } " >
        <div class="title-head">
      <input type="checkbox"  v-model="assignment.status" />
      <h2>{{ assignment.title }}</h2>
    </div>
      <p>Due Date: {{ assignment.dueDate }}</p>
      <p>Days Remaining: {{ daysRemainings(assignment.dueDate) }}</p>
      <p>Percentage Completed: {{ assignment.percentComplete }}%</p>
      </span>
    </li>
  </ul>

  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? "Show All" : "Hide Completed" }}
  </button>
</template>

<style scoped>
h1 {
  width: 100%;
}
.winning {
  color: green;
}
.losing {
  color: red;
}

.done {
  text-decoration: line-through;
}

.title-head {
  display: flex;
  justify-content: flex-start;
}

ul{
  list-style: none;
  padding: 5px;
}
li{
  padding: 5px;
  margin: 5px;
  border: 1px solid #000;
  border-radius: 5px;
}

button {
  margin-top: 10px;
  padding: 5px;
  border-radius: 5px;
  background-color: #f0f0f0;
  cursor: pointer;
  width: 120px;
}

</style>
