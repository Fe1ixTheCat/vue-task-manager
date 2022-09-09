<template>
  <div class="top">
    <h1>add new task:</h1>
    <input
      maxlength="22"
      type="text" 
      :value="inputValue" 
      @input="handlyInput" 
      @keypress.enter="addTask"
    />
    <button @click="addTask">add</button>
  </div>
  <div class="list">
    <p class="header-list">Active tasks: <b>{{ activeList.length }}</b></p>
    <ul class="active-list" v-if="activeList.length">
      <li 
        v-for="(item, index) in activeList"
        :key="item.id"
      >
        <input type="checkbox" @change="completeTast(item, index)">
        <p><b>{{ index }}</b> {{ item.name }}</p>
        <button @click="removeTask(index, 'active')">remove</button>
      </li>

    </ul>
    <hr />
    <p class="header-list">Complete tasks: <b>{{ completeList.length }}</b></p>
    <ul class="complete-list" v-if="completeList.length">
    <li 
      v-for="(item, index) in completeList"
      :key="item.id"
    >
      <input type="checkbox" @change="cancelTask(item, index)" checked>
      <p><b>{{ index }}</b> {{ item.name }}</p>
      <button @click="removeTask(index, 'complete')">remove</button>
    </li>

    </ul>
  </div>
</template>

<style lang="less">
  @import "../assets/styles/styles.less";
</style>

<script>
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      inputValue: '',
      activeList: [],
      completeList: []
    }
  },
  methods: {
    addTask() {
      if (this.inputValue === '') { return; }
      this.activeList.push({
        name: this.inputValue,
        id: Date.now() + Math.random()
      })
      this.inputValue = '';
    },
    handlyInput(event) {
      this.inputValue = event.target.value;
    },
    completeTast(item, index) {
      this.activeList.splice(index, 1);
      this.completeList.push(item);
    },
    cancelTask(item, index) {
      this.completeList.splice(index, 1);
      this.activeList.push(item);
    },
    removeTask(index, type) {
      type === 'active' ? this.activeList.splice(index, 1) : this.completeList.splice(index, 1)
    },
  }
}
</script>
