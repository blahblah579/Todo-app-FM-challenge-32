<template>
  <!-- LIGHT MODE -->
  <v-container v-if="theme" fluid class="body-main px-0">
    <v-row class="body1 d-flex justify-center pa-0 px-3">
      <v-col cols="12" sm="8" md="5">
        <v-col cols="12" class="body">
          <div class="head d-flex justify-space-between align-center">
            <div class="heading">TODO</div>
            <div class="theme">
              <img
                @click="theme = !theme"
                class="img1 d-block"
                src="/src/assets/icon-moon.svg"
                alt=""
              />
            </div>
          </div>
          <div class="todo-input px-5 py-2">
            <span class="hollow-circle" @click="addTask()"></span>
            <input
              type="text"
              class="task-input"
              v-model="newTask"
              placeholder="Create a new todo..."
              @keyup.enter="addTask"
            />
          </div>
          <div class="list">
            <div class="tasks-list mt-5">
              <div class="task-list" @dragover.prevent @drop="handleDrop">
                <div
                  v-for="(task, index) in filteredTasks"
                  :key="task.id"
                  class="task-row"
                  draggable="true"
                  @dragstart="handleDragStart(index)"
                  @dragend="handleDragEnd"
                  @dragover.prevent
                  @drop="(event) => handleDrop(event, index)"
                >
                  <div class="d-flex align-center justify-space-between">
                    <div class="px-5 mb-3 mt-4 details d-flex align-center">
                      <span
                        :class="[
                          task.isCompleted
                            ? 'task-circle-checked'
                            : 'task-circle',
                        ]"
                        @click="toggleTask(task)"
                      >
                        <img
                          v-if="task.isCompleted"
                          src="/src/assets/icon-check.svg"
                          alt="Completed"
                        />
                      </span>
                      <span
                        :class="['task-desc', { completed: task.isCompleted }]"
                      >
                        {{ task.description }}
                      </span>
                    </div>
                    <v-icon
                      class="grid2"
                      icon="mdi-unfold-more-horizontal"
                      size="large"
                    ></v-icon>
                  </div>
                  <div class="line"></div>
                </div>
              </div>
            </div>
            <div
              class="footer-controls d-flex align-center justify-space-between px-5 my-4"
            >
              <span class="left">{{ tasksLeft }} items left</span>

              <div class="filter-buttons d-none d-md-flex pl-10">
                <button
                  @click="filter = 'all'"
                  :class="[filter === 'all' ? 'all-active' : 'all']"
                >
                  All
                </button>
                <button
                  @click="filter = 'active'"
                  :class="[filter === 'active' ? 'active-active' : 'active']"
                >
                  Active
                </button>
                <button
                  @click="filter = 'completed'"
                  :class="[
                    filter === 'completed' ? 'complete-active' : 'complete',
                  ]"
                >
                  Completed
                </button>
              </div>

              <button @click="clearCompleted" class="clear d-flex align-center">
                Clear Completed
              </button>
            </div>
          </div>

          <div class="list12 d-flex justify-center align-center d-md-none mt-4">
            <div class="my-4">
              <div class="filter-buttons d-flex">
                <button
                  @click="filter = 'all'"
                  :class="[filter === 'all' ? 'all-active' : 'all']"
                >
                  All
                </button>
                <button
                  @click="filter = 'active'"
                  :class="[filter === 'active' ? 'active-active' : 'active']"
                  class="mx-5"
                >
                  Active
                </button>
                <button
                  @click="filter = 'completed'"
                  :class="[
                    filter === 'completed' ? 'complete-active' : 'complete',
                  ]"
                >
                  Completed
                </button>
              </div>
            </div>
          </div>
          <div class="message2 d-flex justify-center">
            Drag and drop to reorder list
          </div>
        </v-col>
      </v-col>
    </v-row>
  </v-container>

  <!-- DARK MODE -->
  <v-container v-if="!theme" fluid class="body-main2 px-0">
    <v-row class="body12 d-flex justify-center pa-0 px-3">
      <v-col cols="12" sm="8" md="5">
        <v-col cols="12" class="body">
          <div class="head d-flex justify-space-between align-center">
            <div class="heading">TODO</div>
            <div class="theme">
              <img
                @click="theme = !theme"
                class="img1 d-block"
                src="/src/assets/icon-sun.svg"
                alt=""
              />
            </div>
          </div>
          <div class="todo-input2 px-5 py-2 d-flex align-center">
            <span class="hollow-circle2" @click="addTask()"></span>
            <input
              type="text"
              class="task-input2"
              v-model="newTask"
              placeholder="Create a new todo..."
              @keyup.enter="addTask"
            />
          </div>

          <div class="list2">
            <div class="tasks-list mt-5">
              <div class="task-list" @dragover.prevent @drop="handleDrop">
                <div
                  v-for="(task, index) in filteredTasks"
                  :key="task.id"
                  class="task-row"
                  draggable="true"
                  @dragstart="handleDragStart(index)"
                  @dragend="handleDragEnd"
                  @dragover.prevent
                  @drop="(event) => handleDrop(event, index)"
                >
                  <div class="d-flex align-center justify-space-between">
                    <div class="px-5 mb-3 mt-4 details d-flex align-center">
                      <span
                        :class="[
                          task.isCompleted
                            ? 'task-circle-checked'
                            : 'task-circle2',
                        ]"
                        @click="toggleTask(task)"
                      >
                        <img
                          v-if="task.isCompleted"
                          src="/src/assets/icon-check.svg"
                          alt="Completed"
                        />
                      </span>
                      <span
                        :class="['task-desc2', { completed: task.isCompleted }]"
                      >
                        {{ task.description }}
                      </span>
                    </div>
                    <v-icon
                      class="grid"
                      icon="mdi-unfold-more-horizontal"
                      size="large"
                    ></v-icon>
                  </div>
                  <div class="line2"></div>
                </div>
              </div>
            </div>
            <div
              class="footer-controls d-flex align-center justify-space-between px-5 my-4"
            >
              <span class="left">{{ tasksLeft }} items left</span>

              <div class="filter-buttons d-none d-md-flex pl-10">
                <button
                  @click="filter = 'all'"
                  :class="[filter === 'all' ? 'all-active' : 'all']"
                >
                  All
                </button>
                <button
                  @click="filter = 'active'"
                  :class="[filter === 'active' ? 'active-active' : 'active']"
                >
                  Active
                </button>
                <button
                  @click="filter = 'completed'"
                  :class="[
                    filter === 'completed' ? 'complete-active' : 'complete',
                  ]"
                >
                  Completed
                </button>
              </div>

              <button @click="clearCompleted" class="clear d-flex align-center">
                Clear Completed
              </button>
            </div>
          </div>
          <div class="list22 d-flex justify-center align-center d-md-none mt-4">
            <div class="my-4">
              <div class="filter-buttons d-flex">
                <button
                  @click="filter = 'all'"
                  :class="[filter === 'all' ? 'all-active' : 'all']"
                >
                  All
                </button>
                <button
                  @click="filter = 'active'"
                  :class="[filter === 'active' ? 'active-active' : 'active']"
                  class="mx-5"
                >
                  Active
                </button>
                <button
                  @click="filter = 'completed'"
                  :class="[
                    filter === 'completed' ? 'complete-active' : 'complete',
                  ]"
                >
                  Completed
                </button>
              </div>
            </div>
          </div>

          <div class="message d-flex justify-center">
            Drag and drop to reorder list
          </div>
        </v-col>
      </v-col>
    </v-row>
  </v-container>
</template>
  
  <script setup>
import { ref, computed } from "vue";
import { v4 as uuidv4 } from "uuid";
// Reactive state for tasks and input field
const theme = ref(true);
const tasks = ref([]);
const newTask = ref("");
const filter = ref("all");

// Add a new task with unique ID
const addTask = () => {
  if (newTask.value.trim() === "") return;

  tasks.value.push({
    id: uuidv4(),
    description: newTask.value.trim(),
    isCompleted: false,
  });
  newTask.value = ""; // Clear input field
};

// Toggle task completion
const toggleTask = (task) => {
  task.isCompleted = !task.isCompleted;
};

// Clear completed tasks
const clearCompleted = () => {
  tasks.value = tasks.value.filter((task) => !task.isCompleted);
};

// Computed properties for filtering and counting tasks
const filteredTasks = computed(() => {
  if (filter.value === "active")
    return tasks.value.filter((task) => !task.isCompleted);
  if (filter.value === "completed")
    return tasks.value.filter((task) => task.isCompleted);
  return tasks.value;
});

const tasksLeft = computed(
  () => tasks.value.filter((task) => !task.isCompleted).length
);
// DRAG PART
let draggedTaskIndex = null;

const handleDragStart = (index) => {
  draggedTaskIndex = index;
};

const handleDrop = (event, dropIndex) => {
  const draggedTask = filteredTasks.value[draggedTaskIndex];

  // If the task is dropped on itself, do nothing
  if (draggedTaskIndex === dropIndex) return;

  let prev = draggedTask;

  if (dropIndex > draggedTaskIndex) {
    for (let i = dropIndex; i >= draggedTaskIndex; i--) {
      [prev, filteredTasks.value[i]] = [filteredTasks.value[i], prev];
    }
    return;
  }

  for (let i = dropIndex; i <= draggedTaskIndex; i++) {
    [prev, filteredTasks.value[i]] = [filteredTasks.value[i], prev];
  }

  draggedTaskIndex = null;
};

const handleDragEnd = () => {
  draggedTaskIndex = null; // Reset index after drag ends
};
</script>
  
  <style scoped>
@font-face {
  font-family: f1;
  src: url(/src/assets/JosefinSans-SemiBold.ttf);
}
@font-face {
  font-family: f2;
  src: url(/src/assets/JosefinSans-Regular.ttf);
}
@font-face {
  font-family: f3;
  src: url(/src/assets/JosefinSans-Medium.ttf);
}
* {
  color: hsl(234, 15%, 25%);
}
.task-list {
  cursor: pointer;
}
.body-main {
  height: 100%;
  width: 100vw;
  background-color: hsl(0, 0%, 98%);
}
.body-main2 {
  height: 100%;
  width: 100vw;
  background-color: hsl(240, 20%, 12%);
}
.body1 {
  background-image: url("/src/assets/bg-desktop-light.jpg");
  background-position: top center;
  background-repeat: no-repeat;
  background-size: contain;
  margin-top: -30px;
}
.body12 {
  background-image: url("/src/assets/bg-desktop-dark.jpg");
  background-position: top center;
  background-repeat: no-repeat;
  background-size: contain;
  margin-top: -30px;
}
.body {
  margin-top: 50px;
  margin-bottom: 100px;
}
.heading {
  color: white;
  font-size: 35px;
  font-family: f1;
  letter-spacing: 10px;
}
.todo-input {
  display: flex;
  align-items: center;
  margin-top: 20px;
  background-color: white;
  border-radius: 5px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1);
}
.todo-input2 {
  margin-top: 20px;
  background-color: hsl(235, 24%, 19%);
  border-radius: 5px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1);
}
.todo-input input {
  outline: none;
  border: none;
  box-shadow: none;
}
.hollow-circle {
  width: 22px;
  height: 22px;
  border: 1.5px solid hsl(240, 5%, 93%);
  border-radius: 50%;
  cursor: pointer;
}
.hollow-circle2 {
  width: 22px;
  height: 22px;
  border: 1.5px solid hsl(235, 19%, 24%);
  border-radius: 50%;
  cursor: pointer;
}

.task-input {
  font-size: 16px;
  font-family: f2;
  flex: 1;
  margin-left: 10px;
  padding: 10px;
  border-radius: 10px;
  border: none;
}
.task-input2 {
  font-size: 16px;
  font-family: f2;
  flex: 1;
  margin-left: 10px;
  padding: 10px;
  border-radius: 10px;
  border: none;
  color: hsl(236, 32%, 83%);
}
.task-input:focus,
.task-input2:focus {
  outline: none;
}
.task-input::placeholder {
  font-family: f2;
  font-size: 16px; /* Adjust font size */
  font-weight: 300; /* Adjust font weight */
  color: hsl(252, 2%, 51%); /* Adjust color */
  opacity: 0.7; /* Control placeholder transparency */
}

.task-circle {
  width: 22px;
  height: 22px;
  border: 1.5px solid hsl(236, 33%, 92%);
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.task-circle2 {
  width: 22px;
  height: 22px;
  border: 1.5px solid hsl(235, 20%, 23%);
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.task-circle-checked {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background: linear-gradient(135deg, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}

.task-desc {
  margin-left: 23px;
  font-size: 16px;
}
.task-desc2 {
  color: hsl(236, 32%, 83%);
  margin-left: 23px;
  font-size: 16px;
}

.completed {
  color: hsla(240, 1%, 82%, 50%);
  text-decoration: line-through;
}
.filter-buttons button {
  margin: 0px 8px 0px 8px;
  cursor: pointer;
}
.list {
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1); /* Stronger shadow */
  padding-bottom: 0.5px;
}
.list12 {
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1); /* Stronger shadow */
}
.list22 {
  background-color: hsl(235, 24%, 19%);
  border-radius: 5px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1); /* Stronger shadow */
}
.list2 {
  background-color: hsl(235, 24%, 19%);
  border-radius: 5px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1); /* Stronger shadow */
  padding-bottom: 0.5px;
}
.img1 {
  cursor: pointer;
  scale: 0.8;
}
.tasks-list {
  padding-top: 1px;
  font-family: f2;
}
.left,
.clear {
  font-family: f3;
  color: hsl(252, 7%, 71%);
  font-size: 12px;
}
.left2,
.clear2 {
  font-family: f3;
  color: hsl(236, 16%, 35%);
  font-size: 12px;
}
.active,
.all,
.complete {
  font-family: f1;
  color: hsl(253, 5%, 62%);
  font-size: 14px;
}
.active2,
.all2,
.complete2 {
  font-family: f1;
  color: hsl(236, 16%, 35%);
  font-size: 14px;
}
.active-active,
.all-active,
.complete-active {
  font-family: f1;
  color: hsl(220, 63%, 55%);
  font-size: 14px;
}
.line {
  width: 100%; /* Full width */
  height: 1px; /* Thickness of the line */
  background-color: hsl(255, 9%, 91%); /* Line color */
}
.line2 {
  width: 100%; /* Full width */
  height: 1px; /* Thickness of the line */
  background-color: hsl(235, 17%, 26%); /* Line color */
}
.grid {
  color: transparent;
  padding-right: 30px;
}
.grid2 {
  color: transparent;
  padding-right: 30px;
}
.task-row:hover .grid2 {
  color: hsla(255, 9%, 91%, 70%);
  transition: color 0.3s ease;
}
.task-row:hover .grid {
  color: hsla(236, 6%, 42%, 20%);
  transition: color 0.3s ease;
}
.message {
  margin-top: 50px;
  font-size: 12px;
  color: hsl(236, 13%, 41%);
  font-family: f3;
}
.message2 {
  margin-top: 50px;
  font-size: 12px;
  color: hsl(240, 3%, 58%);
  font-family: f3;
}
@media (max-width: 599.5px) {
  .body1 {
    background-image: url("/src/assets/bg-mobile-light.jpg");
    background-position: top center;
    background-repeat: no-repeat;
    background-size: contain;
    margin-top: -30px;
  }
  .body12 {
    background-image: url("/src/assets/bg-mobile-dark.jpg");
    background-position: top center;
    background-repeat: no-repeat;
    background-size: contain;
    margin-top: -30px;
  }
  .body {
    margin-top: 50px;
    margin-bottom: 200px;
  }
  .active,
  .all,
  .complete {
    font-family: f1;
    color: hsl(253, 5%, 62%);
    font-size: 16px;
  }
  .active2,
  .all2,
  .complete2 {
    font-family: f1;
    color: hsl(236, 16%, 35%);
    font-size: 16px;
  }
  .active-active,
  .all-active,
  .complete-active {
    font-family: f1;
    color: hsl(220, 63%, 55%);
    font-size: 16px;
  }
  .left,
  .clear {
    font-family: f3;
    color: hsl(252, 7%, 71%);
    font-size: 15px;
  }
  .left2,
  .clear2 {
    font-family: f3;
    color: hsl(236, 16%, 35%);
    font-size: 15px;
  }
}
@media (min-width: 599.5px) and (max-width: 959.5px) {
  .body1 {
    background-image: url("/src/assets/bg-desktop-light.jpg");
    background-position: top center;
    background-repeat: no-repeat;
    background-size: contain;
    margin-top: -30px;
    background-size: 135%;
  }
  .body12 {
    background-image: url("/src/assets/bg-desktop-dark.jpg");
    background-position: top center;
    background-repeat: no-repeat;
    background-size: contain;
    margin-top: -30px;
    background-size: 135%;
  }
}
</style>
  