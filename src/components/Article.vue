<template>
  <div :class="`article-${mode}`">
    <ArticleHeader :categories="article.categories"></ArticleHeader>
    <ArticleContent :article="article" :mode="mode" />
  </div>
</template>

<script>
import ArticleHeader from "@/components/ArticleHeader.vue";
import ArticleContent from "@/components/ArticleContent.vue";

export default {
  components: {
    ArticleHeader,
    ArticleContent
  },
  props: {
    mode: {
      type: String,
      validator: prop => ["headline", "featured", "default"].includes(prop)
    },
    article: Object
  }
};
</script>

<style scoped>
.article-headline,
.article-featured {
  position: relative;
  pointer-events: auto;
}
.article-headline {
  align-self: flex-start;
  margin: 5px;
  top: 0px;
  left: 0px;
  margin-top: 0;
  flex-grow: 1;
}

.article-default {
  padding-top: 2em;
}

.article-default,
.article-featured {
  margin: 10px;
  margin-top: 0;
}

@media (max-width: 750px) {
  .article-featured,
  .article-default {
    margin: 0;
    margin-bottom: 1em;
    max-width: 295px;
    min-height: 0;
  }
}
</style>
