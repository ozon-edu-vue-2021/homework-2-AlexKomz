<template>
  <div
      class="container"
      tabindex="0"
      :class="{ 'container_selected': isSelected }"
      @click="setSelectedItem(fullPath)"
      @keydown="pressEnterHandler"
  >
    <slot/>
  </div>
</template>

<script>
export default {
  name: "TypeBase",
  props: {
    name: {
      type: String,
      required: true
    },
    path: {
      type: String,
      required: true
    },
    isSelected: {
      type: Boolean,
      required: true
    }
  },
  inject: {
    setSelectedItem: {
      from: `setSelectedItem`
    }
  },
  computed: {
    fullPath() {
      return `${this.path}${this.name}`;
    }
  },
  methods: {
    pressEnterHandler(event) {
      if (event.key === `Enter`) {
        this.setSelectedItem(this.fullPath);
      }
    }
  }
}
</script>
