<template>
  <div :class="`image ${loadingClass}`" :style="image"><slot /></div>
</template>

<script>
export default {
  props: {
    url: {
      type: String,
      default: ""
    },
    loader: {
      type: Boolean,
      default: true
    },
    noimage: {
      type: String,
      default: "noimage"
    }
  },
  data() {
    return {
      image: "",
      loaded: false
    };
  },
  created() {
    if (this.loader) {
      this.image = `background-image: url(${require("../assets/loading.gif")}); background-size: 18px; transition-property: none !important;`;
    }
  },
  mounted() {
    this.loadImage();
  },
  computed: {
    loadingClass() {
      return !this.loaded ? "loading" : "";
    }
  },
  methods: {
    loadImage() {
      let im = new Image();
      im.onerror = () => {
        if (this.noimage === "user")
          this.image = `background-image: url(${require("../assets/nophoto.png")});`;
        else {
          this.image = `background-image: url(${require("../assets/noimage.jpg")});`;
        }
      };
      im.onload = () => {
        this.image = `background-image: url(${this.url});`;
        setTimeout(() => {
          this.loaded = true;
        }, 500);
      };
      im.src = this.url;
    }
  }
};
</script>

<style scoped>
.image {
  background-position: center center;
  background-size: cover;
  background-repeat: no-repeat;
}
.image.loading {
  transition-property: none !important;
}
</style>
