<template>
  <div id="app">
    <div>
      <input
        type="checkbox"
        id="dragAndDropActive"
        name="dragAndDropActive"
        v-model="dragAndDropActive"
      />
      <label for="dragAndDropActive">dragAndDropActive</label>
    </div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <DraggableForm
      :drag-and-drop-active="dragAndDropActive"
      :formData="formData"
    />
    <pre>{{ formData }}</pre>
  </div>
</template>

<script>
import DraggableForm from "./components/DraggableForm.vue";

export default {
  name: "App",
  components: {
    DraggableForm,
  },
  data: () => ({
    dragAndDropActive: false,
    formData: {
      id: "form1",
      inputFieldSets: [
        {
          ids: ["apple", "banana"],
        },
        {
          ids: ["strawberry"],
        },
        {
          ids: ["orange", "kiwi"],
        },
      ],
    },
  }),
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

pre {
  text-align: left;
}
</style>
