<template>
  <div class="subject" :style="`color: ${color};`">
    {{ text }}
  </div>
</template>

<script>
export default {
  props: {
    text: {
      type: String
    },
    color: {
      type: String,
      default: "black"
    }
  }
};
</script>
<style scoped>
div.subject {
  margin-bottom: 8px;
}
@media (max-width: 750px) {
  div.subject {
    font-size: 10px;
  }
}
</style>
