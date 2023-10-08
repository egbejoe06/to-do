<template>
  <div class="main">
    <div :class="{ changebg: changebg, bg1: bg1 }">
      <span class="todo">TODO</span>
      <span @click="change()"> <img :src="Image" alt="image" /> </span>
    </div>
    <div :class="{ bg2: bg2, changebg2: changebg2 }">
      <div class="todos">
        <div :class="{ tasks: tasks, tasks2: tasks2 }">
          <input
            v-model="check"
            class="inp-cbx"
            id="cbx-15"
            type="checkbox"
            style="display: none"
          />
          <label @click="addtask" class="cbx" for="cbx-15">
            <span>
              <svg width="12px" height="9px" viewbox="0 0 12 9">
                <polyline points="1 5 4 8 11 1"></polyline>
              </svg>
            </span>
          </label>
          <span class="task"
            ><input
              v-model="Task"
              @keyup.enter="addtask2()"
              type="text"
              placeholder="current typing"
              :class="{ input: input, input2: input2 }"
          /></span>
        </div>
        <div>
          <All
            :check="check"
            :Task="Task"
            :Todos="Todos"
            :to_do="to_do"
            :to_do2="to_do2"
            :task1="task1"
            :task2="task2"
            :footer1="footer1"
            :footer2="footer2"
            @clear-completed="clearCompletedTodos"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import All from "./components/All.vue";

export default {
  name: "App",
  data() {
    return {
      check: false,
      Task: "",
      Todos: [],
      changebg: false,
      changebg2: false,
      bg1: true,
      bg2: true,
      tasks2: false,
      tasks: true,
      Image: require("./assets/icon-sun.svg"),
      input: true,
      input2: false,
      to_do: true,
      to_do2: false,
      task1: true,
      task2: false,
      footer1: true,
      footer2: false,
    };
  },
  components: { All },
  methods: {
    addtask2() {
      if (this.check == false && this.Task) {
        const taskExists = this.Todos.some((todo) => todo.taask === this.Task);

        if (!taskExists) {
          this.Todos.push({ taask: this.Task, isChecked: false, completed: false });
        }
        this.Task = "";
      }
    },
    addtask() {
      if (this.check == false && this.Task) {
        const taskExists = this.Todos.some((todo) => todo.taask === this.Task);

        if (!taskExists) {
          this.Todos.push({ taask: this.Task, isChecked: false, completed: false });
        }
        this.Task = "";
      }
      this.check = true;
    },
  },
  change() {
    this.changebg = !this.changebg;
    this.bg1 = !this.bg1;
    this.changebg2 = !this.changebg2;
    this.bg2 = !this.bg2;
    this.tasks = !this.tasks;
    this.tasks2 = !this.tasks2;
    this.input = !this.input;
    this.input2 = !this.input2;
    this.to_do = !this.to_do;
    this.to_do2 = !this.to_do2;
    this.task1 = !this.task1;
    this.task2 = !this.task2;
    this.footer1 = !this.footer1;
    this.footer2 = !this.footer2;
    this.Image =
      this.Image === require("./assets/icon-sun.svg")
        ? require("./assets/icon-moon.svg")
        : require("./assets/icon-sun.svg");
  },
  clearCompletedTodos() {
    this.Todos = this.Todos.filter((todo) => !todo.completed);
  },
};
</script>
<style>
@media (max-width: 375px) {
  .footer1 {
    display: flex;
    gap: 15px;
    position: relative;
    top: 30px;
    border-radius: 10px;
    background-color: hsl(235, 24%, 19%);
    width: 200px;
    padding: 10px;
    justify-content: center;
    left: 7px;
  }
  .footer2 {
    display: flex;
    gap: 15px;
    position: relative;
    top: 30px;
    border-radius: 10px;
    background-color: hsl(0, 0%, 98%);
    width: 200px;
    padding: 10px;
    justify-content: center;
    left: 7px;
  }
  .footer {
    gap: 0px;
  }
  .f_clear {
    position: relative;
    left: -10px;
  }
  .f_items {
    position: relative;
    left: 13px;
  }
  .bg11 {
    left: 30px;
  }
  .changebg {
    gap: 190px !important;
  }
  .bg1 {
    gap: 190px !important;
  }
}
* {
  box-sizing: border-box;
  margin: 0;
  transition: 0.5s;
  font-family: "Josefin Sans", sans-serif;
}
.input2 {
  width: 220px;
  background-color: transparent;
  border: none;
  padding: 8px;
  color: hsl(235, 19%, 35%);
  outline: none;
}
.tasks2 {
  border-radius: 10px;
  background-color: hsl(0, 0%, 98%);
  width: 300px;
  padding: 5px;
}
.changebg2 {
  background-color: hsl(226.41deg 43% 95% / 74%);
  width: 100%;
  height: 100%;
}
.changebg {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 250px;
  height: 150px;
  width: 100%;
  background-image: url(./assets/bg-desktop-light.jpg);
}
.tasks {
  border-radius: 10px;
  background-color: hsl(235, 24%, 19%);
  width: 300px;
  padding: 5px;
}
.task {
  width: 100px;
  padding: 10px;
}
.input {
  width: 220px;
  background-color: transparent;
  border: none;
  padding: 8px;
  color: white;
  outline: none;
}
.bg1 {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 250px;
  height: 150px;
  width: 100%;
  background-image: url(./assets/bg-desktop-dark.jpg);
}
.bg2 {
  background-color: hsl(235, 21%, 11%);
  width: 100%;
  height: 100%;
}
.todos {
  display: flex;
  flex-direction: column;
  gap: 20px;
  position: relative;
  justify-content: center;
  align-items: center;
  top: -45px;
}
.todo {
  font-size: 30px;
  color: hsl(0, 0%, 98%);
}
.inp-cbx {
  display: none;
}

.cbx {
  -webkit-user-select: none;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
  cursor: pointer;
}

.cbx span {
  display: inline-block;
  vertical-align: middle;
  transform: translate3d(0, 0, 0);
}

.cbx span:first-child {
  position: relative;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  transform: scale(1);
  vertical-align: middle;
  border: 1px solid #b9b8c3;
  transition: all 0.2s ease;
}

.cbx span:first-child svg {
  position: absolute;
  z-index: 1;
  top: 8px;
  left: 6px;
  fill: none;
  stroke: white;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-dasharray: 16px;
  stroke-dashoffset: 16px;
  transition: all 0.3s ease;
  transition-delay: 0.1s;
  transform: translate3d(0, 0, 0);
}

.cbx span:first-child:before {
  content: "";
  width: 100%;
  height: 100%;
  background: #506eec;
  display: block;
  transform: scale(0);
  opacity: 1;
  border-radius: 50%;
  transition-delay: 0.2s;
}

.cbx:hover span:first-child {
  border-color: #3c53c7;
}

.inp-cbx:checked + .cbx span:first-child {
  border-color: red;
  background-color: hsl(234, 39%, 85%);
  animation: check-15 0.6s ease;
}

.inp-cbx:checked + .cbx span:first-child svg {
  stroke-dashoffset: 0;
}

.inp-cbx:checked + .cbx span:first-child:before {
  transform: scale(2.2);
  opacity: 0;
  transition: all 0.6s ease;
}

.inp-cbx:checked + .cbx span:last-child {
  color: #b9b8c3;
  transition: all 0.3s ease;
}

.inp-cbx:checked + .cbx span:last-child:after {
  transform: scaleX(1);
  transition: all 0.3s ease;
}

@keyframes check-15 {
  50% {
    transform: scale(1.2);
  }
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
