<template>
  <div>
    <div class="bg11">
      <div
        :class="{ to_do: to_do, to_do2: to_do2 }"
        v-for="(Todo, index) in filteredTodos"
        :key="index"
        draggable="true"
        @dragstart="dragStart(index)"
        @dragover.prevent
        @drop="drop(index)"
      >
        <span class="todo-span">
          <div class="checkbox_style">
            <div class="checkbox-wrapper-18">
              <div class="round">
                <input
                  type="checkbox"
                  :id="'checkbox-' + index"
                  v-model="Todo.isChecked"
                  @change="toggleCompleted(index)"
                />
                <label :for="'checkbox-' + index"></label>
              </div>
            </div>
          </div>
          <li :class="{ task1: task1, task2: task2, completed: Todo.completed }">
            {{ Todo.taask }}
          </li>
          <div class="cancel" @click="del(index)">
            <img style="width: 15px" src="../assets/icon-cross.svg" alt="" />
          </div>
        </span>
      </div>
    </div>
    <div class="footer">
      <div class="f_items">{{ filteredTodos.length }} items left</div>
      <div :class="{ footer1: footer1, footer2: footer2 }">
        <div
          class="f_all"
          @click="fAll()"
          :style="{ color: activeFilter === 'all' ? (to_do2 ? 'red' : 'blue') : '' }"
        >
          All
        </div>
        <div
          class="f_active"
          @click="fActive()"
          :style="{ color: activeFilter === 'active' ? (to_do2 ? 'red' : 'blue') : '' }"
        >
          Active
        </div>
        <div
          class="f_completed"
          @click="fCompleted()"
          :style="{
            color: activeFilter === 'completed' ? (to_do2 ? 'red' : 'blue') : '',
          }"
        >
          Completed
        </div>
      </div>
      <div class="f_clear" @click="fClear()">Clear Completed</div>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    "Todos",
    "check",
    "Task",
    "to_do",
    "to_do2",
    "task1",
    "task2",
    "footer1",
    "footer2",
  ],
  data() {
    return {
      filteredTodos: this.Todos,
      activeFilter: "all",
    };
  },
  watch: {
    Todos(newTodos) {
      // Update the filteredTodos data property whenever Todos changes
      this.filteredTodos = newTodos.filter((todo) => !todo.completed);
    },
  },
  methods: {
    toggleCompleted(index) {
      this.Todos[index].completed = !this.Todos[index].completed;
    },
    del(index) {
      this.filteredTodos.splice(index, 1);
    },
    fActive() {
      this.filteredTodos = this.Todos.filter((todo) => !todo.completed);
      this.activeFilter = "active";
    },
    fCompleted() {
      this.filteredTodos = this.Todos.filter((todo) => todo.completed);
      this.activeFilter = "completed";
    },
    fAll() {
      this.filteredTodos = this.Todos;
      this.activeFilter = "all";
    },
    fClear() {
      this.$emit("clear-completed");
    },

    dragStart(index) {
      this.draggedItemIndex = index; // Store the index of the dragged item
    },

    drop(targetIndex) {
      // Ensure the target index is not the same as the dragged index
      if (targetIndex !== this.draggedItemIndex) {
        // Splice the item from its current position and insert it at the target index
        const draggedItem = this.filteredTodos.splice(this.draggedItemIndex, 1)[0];
        this.filteredTodos.splice(targetIndex, 0, draggedItem);
        this.draggedItemIndex = null; // Reset the draggedItemIndex
      }
    },
  },
};
</script>

<style>
.f_active,
.f_all,
.f_completed,
.f_clear {
  cursor: pointer;
}
.f_active:hover,
.f_all:hover,
.f_completed:hover,
.f_clear:hover {
  color: hsl(236, 33%, 92%);
}
.footer1,
.footer2 {
  display: flex;
  gap: 5px;
}
.to_do2 {
  border-radius: 10px;
  background-color: hsl(0, 0%, 98%);
  width: 300px;
  text-align: left;
  padding-bottom: 5px;
  padding: 5px;
}
.footer {
  font-size: 13px;
  display: flex;
  gap: 20px;
  margin-top: 20px;
}
.cancel {
  position: relative;
  left: 22px;
  width: 15px;
  top: 8px;
  cursor: pointer;
}
.checkbox_style {
  position: relative;
  left: -7px;
  top: 6px;
}
.task1 {
  background-color: transparent;
  border: none;
  padding: 8px;
  color: white;
  outline: none;
  font-size: 15px;
  list-style: none;
  overflow: auto;
  width: 200px;
}
.task2 {
  background-color: transparent;
  border: none;
  padding: 8px;
  color: hsl(235, 19%, 35%);
  outline: none;
  font-size: 15px;
  list-style: none;
  overflow: auto;
  width: 200px;
}
.to_do {
  border-radius: 10px;
  background-color: hsl(235, 24%, 19%);
  width: 300px;
  text-align: left;
  padding-bottom: 5px;
  padding: 5px;
}

.todo-span {
  position: relative;
  left: 20px;
  display: flex;
}

.bg11 {
  display: flex;
  flex-direction: column;
  gap: 10px;
  position: relative;
  left: 10px;
}

.checkbox-wrapper-18 .round {
  position: relative;
}
.checkbox-wrapper-18 .round label {
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 50%;
  cursor: pointer;
  height: 20px;
  width: 20px;
  display: block;
}

.checkbox-wrapper-18 .round label:after {
  border: 2px solid #fff;
  border-top: none;
  border-right: none;
  content: "";
  height: 4px;
  left: 4px;
  opacity: 0;
  position: absolute;
  top: 6px;
  transform: rotate(-45deg);
  width: 8px;
}

.checkbox-wrapper-18 .round input[type="checkbox"] {
  visibility: hidden;
  display: none;
  opacity: 0;
}

.checkbox-wrapper-18 .round input[type="checkbox"]:checked + label {
  background-color: #66bb6a;
  border-color: #66bb6a;
}

.checkbox-wrapper-18 .round input[type="checkbox"]:checked + label:after {
  opacity: 1;
}

.completed {
  text-decoration: line-through;
  color: #888;
}
</style>
