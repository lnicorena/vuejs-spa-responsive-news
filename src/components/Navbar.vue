<template>
  <div>
    <section id="navbar">
      <NavbarSidemenu
        :categories="categories"
        @categoryClicked="categorySelected"
      />
      <NavbarLogo
        :categories="categories"
        @logoClicked="categorySelected(0)"
      />
      <NavbarItems
        :categories="categories"
        @categoryClicked="categorySelected"
      />
    </section>
  </div>
</template>
<script>
import NavbarSidemenu from "@/components/NavbarSidemenu.vue";
import NavbarLogo from "@/components/NavbarLogo.vue";
import NavbarItems from "@/components/NavbarItems.vue";

export default {
  props: {
    categories: Array
  },
  components: { NavbarSidemenu, NavbarLogo, NavbarItems },
  methods: {
    categorySelected(id) {
      this.$emit("categorySelected", id);
    }
  }
};
</script>
