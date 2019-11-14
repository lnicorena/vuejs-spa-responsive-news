<template>
  <a :href="url" target="_blank">
    <ArticleImage :class="`article-image-${mode}`" :url="image">
      <ReadMore :mode="mode" />
    </ArticleImage>
    <p :class="`article-title-${mode}`">
      <slot></slot>
    </p>
  </a>
</template>

<script>
import ReadMore from "@/components/ArticleContentNewsRead.vue";
import ArticleImage from "@/components/_image.vue";

export default {
  components: {
    ReadMore,
    ArticleImage
  },
  props: {
    url: {
      type: String,
      default: "#"
    },
    mode: {
      type: String,
      default: "default"
    },
    image: {
      type: String,
      default: ""
    }
  },

  computed: {
    showImage() {
      return this.mode != "default";
    }
  }
};
</script>

<style scoped>
.article-image-featured,
.article-image-headline {
  transition-property: all;
  transition-duration: 0.5s;
  display: flex;
  align-items: center;
  justify-content: center;
}
.article-image-featured {
  width: 295px;
  height: 185px;
}
.article-image-headline {
  width: 555px;
  height: 354px;
}
@media (max-width: 1170px) {
  .article-image-featured {
    width: 350px;
    height: 220px;
  }
  .article-image-headline {
    width: 720px;
    height: 460px;
  }
}
@media (max-width: 750px) {
  .article-image-featured,
  .article-image-headline {
    width: 295px;
    height: 185px;
  }
}

.article-title-headline,
.article-title-featured,
.article-title-default {
  font-size: 19px;
  margin: 0px;
  margin-top: 15px;
  margin-bottom: 8px;
  max-width: 550px;
}
@media (max-width: 1170px) {
  .article-title-headline,
  .article-title-featured,
  .article-title-default {
    max-width: 720px;
  }
}
</style>
