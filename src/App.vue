<template>
  <div id="app">
    <input v-model="inputValue" />
    <div v-if="showError">
      Invalid input value, please enter the name without the first letter "B"
    </div>
    <button @click="addItem">Add item</button>
    <ToDoList :dataList="toDoList" @toggleItem="toggleItemList" />
  </div>
</template>

<script>
import ToDoList from "./components/ToDoList/ToDoList.vue";
import { TO_DO_LIST } from "./constants";

export default {
  components: {
    ToDoList,
  },
  data() {
    return {
      toDoList: TO_DO_LIST,
      inputValue: "",
      showError: false,
    };
  },
  mounted() {
    this.filterList();
  },
  methods: {
    filterList() {
      this.toDoList = this.toDoList.filter(
        (option) => option.name.toLowerCase().substring(0, 1) !== "b"
      );
    },
    toggleItemList(id) {
      this.toDoList = this.toDoList.map((option) => ({
        ...option,
        checked: option.id === id ? !option.checked : option.checked,
      }));
    },
    addItem() {
      if (this.inputValue.toLowerCase().substring(0, 1) !== "b") {
        this.toDoList.push({
          id: Date.now(),
          name: this.inputValue,
          checked: false,
        });
        this.showError = false;
        this.inputValue = "";
      } else {
        this.showError = true;
      }
    },
  },
};
</script>
