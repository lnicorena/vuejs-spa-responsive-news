<template>
  <div class="subject" v-html="categoryName" />
</template>

<script>
export default {
  props: {
    categories: {
      type: Array
    }
  },
  data() {
    return {
      maxCategoriesShow: 2
    };
  },
  computed: {
    categoryName() {
      if (this.categories.length == 0) return "OTHERS";
      else
        return this.filteredCategories
          .map(c => {
            let colors = ["#FF001F", "#4990E2", "#7CBC37", "#F6A623"];
            let color = parseInt(c.id) % 4;
            return `<span style="color: ${
              colors[color]
            };">${c.name.toUpperCase()}</span>`;
          })
          .join(" ");
    },
    filteredCategories() {
      let max =
        this.categories.length <= this.maxCategoriesShow
          ? this.categories.length
          : this.maxCategoriesShow;
      return this.categories.slice(0, max);
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
