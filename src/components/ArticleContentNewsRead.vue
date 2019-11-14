<template>
  <div :class="`read-more-${mode}`"><div>Read More</div></div>
</template>
<script>
export default {
  props: {
    mode: String
  }
};
</script>

<style scoped>
.read-more-default {
  display: none;
}

.read-more-headline,
.read-more-featured {
  text-decoration: none;
  transition-property: all;
  transition-duration: 0.5s;
  font-size: 14px;
  font-weight: bold;
  display: none;
  width: 30%;
  height: 15%;
  text-align: center;
  color: white;
  z-index: 200;
  background-color: rgba(0, 0, 0, 0.8);
  border: 2px solid rgba(255, 255, 255, 0.9);
}

@media (min-width: 750px) {
  .read-more-headline {
    font-size: 120%;
  }
}

.read-more-headline:hover,
.read-more-featured:hover {
  background-color: grey;
}

* > a:hover .read-more-headline,
* > a:hover .read-more-featured {
  display: flex;
  align-items: center;
  justify-content: center;
  animation: fadeIn 0.2s;
}
</style>
