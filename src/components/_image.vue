<template>
  <div class="image" :style="image"><slot /></div>
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
      default: false
    },
    noimage: {
      type: String,
      default: "noimage"
    }
  },
  data() {
    return {
      image: ""
    };
  },
  created() {
    if (this.loader) {
      this.image = `background-image: url(${require("../assets/loading.gif")}); background-size: 18px;`;
    }
  },
  mounted() {
    this.loadImage();
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
</style>
