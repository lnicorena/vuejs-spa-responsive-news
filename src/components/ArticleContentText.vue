<template>
  <div :class="className">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default: ""
    },
    mode: {
      type: String,
      default: "default"
    }
  },

  computed: {
    className() {
      return `article-text-${this.mode}`;
    }
  }
};
</script>

<style scoped>
div[class^="article-text-"] {
  font-size: 14px;
  font-family: "Open Sans", sans-serif;
  font-weight: 590;
  overflow-wrap: break-word;
  color: #686868;
}

.article-text-headline {
  display: none;
}
.article-text-default,
.article-text-featured {
  display: inline;
}

@media (max-width: 750px) {
  div[class^="article-text-"] {
    display: inline;
  }
}
</style>
