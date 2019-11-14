<template>
  <div :class="`article-content-${mode}`">
    <News :mode="mode" :url="article.url" :image="article.image">
      {{ article.title | escape}}
    </News>
    <Author :mode="mode" :image="article.avatar">
      {{ article.author }}
    </Author>
    <TextInfo :mode="mode">
      {{ article.text |  escape | truncate(230) }}
    </TextInfo>
  </div>
</template>

<script>
import Author from "@/components/ArticleContentAuthor.vue";
import News from "@/components/ArticleContentNews.vue";
import TextInfo from "@/components/ArticleContentText.vue";
import TextFilters from "@/components/_filters.vue";

export default {
  components: {
    Author,
    News,
    TextInfo
  },
  props: {
    article: Object,
    mode: String
  },
  mixins: [
    TextFilters
  ],
};
</script>

<style scoped>
* > a {
  text-decoration: none;
  color: black;
}

.article-content-headline,
.article-content-default {
  display: flex;
  flex-direction: column;
}

.article-content-featured {
  max-width: 295px;
}

.article-content-default {
  max-width: 380px;
  min-height: 260px;
}
@media (max-width: 1170px) {
  .article-content-featured,
  .article-content-default {
    margin-bottom: 1em;
    max-width: 350px;
  }
}
@media (max-width: 750px) {
  .article-content-headline,
  .article-content-featured,
  .article-content-default {
    margin-bottom: 1em;
    max-width: 295px;
  }
}
</style>
