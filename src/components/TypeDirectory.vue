<template>
  <div class="wrapper">
    <div
        class="container"
        @click="isOpened = !isOpened"
        @keydown="pressEnter"
        tabindex="0"
    >
      <i class="fas" :class="iconClasses"></i>
      <span class="container__name container__name_directory" :class="{ 'container__name_opened': isOpened }">
        {{ name }}
      </span>
    </div>
    <ul class="list" v-if="isOpened">
      <li v-for="(item, i) of contents" :key="i">
        <type-base
            v-if="item.type === `file`"
            :is-selected="selectedItem === `${fullPath}${item.name}`"
            :name="item.name"
            :path="fullPath"
        >
          <i class="fas fa-file"/>
          <span class="container__name">{{ item.name }}</span>
        </type-base>
        <type-base
            v-else-if="item.type === `link`"
            :is-selected="selectedItem === `${fullPath}${item.name}`"
            :name="item.name"
            :path="fullPath"
        >
          <i class="fas fa-link"></i>
          <span class="container__name container__name_link">{{ item.name }}</span>
        </type-base>
        <type-directory
            v-else
            :is-selected="false"
            :name="item.name"
            :path="fullPath"
            :selectedItem="selectedItem"
            :contents="item.contents"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import TypeBase from "@/components/TypeBase";
import TypeDirectory from "@/components/TypeDirectory";

export default {
  name: "TypeDirectory",
  data: () => ({
    isOpened: false
  }),
  props: {
    name: {
      type: String,
      required: true
    },
    path: {
      type: String,
      required: true
    },
    selectedItem: {
      type: String,
      required: true
    },
    contents: {
      type: Array,
      default: () => ([])
    }
  },
  components: {TypeBase, TypeDirectory},
  computed: {
    iconClasses() {
      return this.isOpened ? `fa-folder-open` : `fa-folder`;
    },
    fullPath() {
      return `${this.path}${this.name}/`;
    }
  },
  methods: {
    pressEnter(event) {
      if (event.key === `Enter`) {
        this.isOpened = !this.isOpened
      }
    }
  }
}
</script>
