<template>
  <div>
    <span>Path: {{ selectedItem }}</span>
    <type-directory
        :name="name"
        path="./"
        :selectedItem="selectedItem"
        :contents="contents"
    />
  </div>
</template>

<script>
import data from "../public/static/node_modules.json";

import TypeDirectory from "@/components/TypeDirectory";

export default {
  name: 'App',
  components: {TypeDirectory},
  provide() {
    return {
      setSelectedItem: this.setSelectedItem
    };
  },
  data() {
    return {
      selectedItem: ``,
      name: ``,
      contents: [],
    };
  },
  created() {
    this.name = data.name;
    this.contents = data.contents;
  },
  methods: {
    setSelectedItem(path) {
      this.selectedItem = path;
    }
  }
}
</script>

<style src="./assets/style.css"/>
