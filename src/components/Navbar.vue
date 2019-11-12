<template>
  <div>
    <section id="navbar">
      <NavbarSidemenu :categories="categories" />
      <NavbarLogo :categories="categories" />
      <NavbarItems :categories="categories" />
    </section>
  </div>
</template>
<script>
import NavbarSidemenu from "@/components/NavbarSidemenu.vue";
import NavbarLogo from "@/components/NavbarLogo.vue";
import NavbarItems from "@/components/NavbarItems.vue";

export default {
  data() {
    return {
      categories: ["POLITICS", "BUSINESS", "TECH", "SCIENCE", "SPORTS"]
    };
  },
  components: { NavbarSidemenu, NavbarLogo, NavbarItems }
};
</script>
