<template>
  <div class="nav-menu">
    <span v-for="c in filteredCategories" v-bind:key="c.id">
      <a @click="categoryClicked(c.id)">{{ c.name | escape | upper }}</a>
    </span>
    <span class="login">
      <a>LOGIN</a>
    </span>
  </div>
</template>

<script>
import TextFilters from "@/components/_filters.vue";
export default {
  props: ["categories"],
  mixins: [TextFilters],
  computed: {
    filteredCategories() {
      if (this.categories.length > 7) {
        return this.categories.slice(0, 7);
      } else {
        return this.categories;
      }
    }
  },
  methods: {
    categoryClicked(id) {
      this.$emit("categoryClicked", id);
    }
  }
};
</script>

<style scoped>
.nav-menu {
  max-width: 900px;
  position: absolute;
  text-align: center;
  margin-bottom: 1em;
  top: 1em;
  right: 130px;
}
@media (max-width: 1170px) {
  .nav-menu {
    display: none;
  }
}
.nav-menu span {
  margin-right: 29px;
  size: 14px;
  color: #3e433e;
  line-height: 17px;
}
.nav-menu span.login {
  margin-right: 0px;
  margin-left: 25px;
  color: #4990e2;
}
.nav-menu span a {
  cursor: pointer;
  white-space: nowrap;
}
</style>
