<template>
  <div id="side-menu">
    <img id="menu" src="../assets/menu.png" />
    <div class="header-menu-dropdown">
      <ul>
        <li
          style="color: 'black'; hyphens: 'auto'"
          v-for="c in categories"
          v-bind:key="c"
        >
          <a>
            {{ c }}
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ["categories"]
};
</script>

<style scoped>
#side-menu {
  display: none;
}
@media (max-width: 1170px) {
  #side-menu {
    position: absolute;
    display: inline;
    z-index: 2;
    top: 1em;
    left: 2em;
  }
}
#side-menu#side-menu:hover .header-menu-dropdown {
  display: block;
  animation: fadeInLeft 0.2s;
}
.header-menu-dropdown {
  width: 100%;
  animation: fadeOutLeft 0.2s;
  z-index: -2;
  display: none;
  position: relative;
  padding-left: 1em;
  background-color: white;
  box-shadow: 2px 2px 2px 2px white;
  top: 1em;
  right: 2em;
}
.header-menu-dropdown ul {
  list-style: none;
  padding: 1px;
}
.header-menu-dropdown li {
  margin-bottom: 1em;
}
.header-menu-dropdown a {
  cursor: pointer;
}
</style>
