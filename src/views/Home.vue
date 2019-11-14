<template>
  <div>
    <Navbar :categories="categories" @categorySelected="filterArticles" />
    <div id="main-container" v-if="loaded">
      <div class="primary">
        <section>
          <Article mode="headline" :article="headlineArticle" />
        </section>
        <section>
          <div class="container-featured">
            <Article
              mode="featured"
              v-for="article in featuredArticles"
              v-bind:key="article.id"
              :article="article"
            />
          </div>
        </section>
      </div>
      <div class="secondary">
        <section>
          <div class="container-default">
            <Article
              mode="default"
              v-for="article in defaultArticles"
              v-bind:key="article.id"
              :article="article"
            />
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Article from "@/components/Article.vue";

export default {
  name: "Home",
  components: {
    Navbar,
    Article
  },
  data() {
    return {
      articlesList: null,
      loaded: false,
      articles: [],
      page: 1,
      categories: [],
      categoryFilter: 0,
    };
  },
  created() {
    this.loadCategories();
  },
  mounted() {
    this.loadArticles();
  },
  computed: {
    headlineArticle() {
      return this.articles.length == 0 ? [] : this.articles[0];
    },
    featuredArticles() {
      if (this.articles.length < 2) return [];
      else
        return this.articles.length == 2
          ? this.articles[1]
          : this.articles.slice(1, 3);
    },
    defaultArticles() {
      if (this.articles.length < 4) return [];
      else return this.articles.slice(3, this.articles.length);
    }
  },
  methods: {
    loadCategories() {
      this.$api.get("/categories").then(res => {
        if (res.statusText == "OK" && res.data.length) {
          this.categories = res.data;
          console.log(this.categories);
        }
      });
    },
    filterArticles(id) {
      this.categoryFilter = id;
      this.loadArticles();
    },
    loadArticles() {
      this.loaded = false;
      let url = `/articles?page=${this.page}&category=${this.categoryFilter}`;
      this.$api.get(url).then(res => {
        if (res.statusText == "OK" && res.data.data.length) {
          this.articlesList = res.data;

          this.articles = this.articlesList.data.map(data => {
            let article = {};
            article.title = data.title;
            article.author = data.authors.length
              ? data.authors[0].name
              : "Unknown";
            article.categories = data.categories;
            article.content = data.content;
            article.text = data.excerpt;
            article.avatar = data.authors.length ? data.authors[0].avatar : "";
            article.image = data.image;
            article.url = data.link;
            return article;
          });

          this.loaded = true;
        }
      });
    }
  }
};
</script>

<style>
#main-container {
  margin: 1%;
  margin-top: 55px;
  padding: 5px;

  flex-flow: column;
  position: relative;
  display: flex;

  z-index: 0;
  pointer-events: auto;

  align-items: center;
  justify-content: center;
  font-size: 15px;
}

.container-featured,
.container-default {
  display: flex;
}

.container-default {
  flex-wrap: wrap;
  justify-content: center;
}

@media (max-width: 750px) {
  .container-featured {
    margin: 0;
  }

  .container-featured,
  .container-default {
    height: auto;
    flex-flow: column;
    justify-content: center;
    align-items: center;
  }
}

.primary {
  height: 525px;
  pointer-events: auto;
  margin: 5px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  position: relative;
  font-size: 15px;
}
.primary:after {
  position: absolute;
  left: 0.75%;
  bottom: 0;
  content: "";
  width: 98%;
  border-bottom: 1px solid #979797;
}

.secondary {
  display: flex;
  padding-top: 3em;
  justify-content: center;
}

@media (max-width: 1170px) {
  .primary {
    margin-bottom: 2em;
  }

  .primary,
  .secondary {
    height: auto;
    margin: 0;
    flex-flow: column;
  }

  .primary:after {
    border: none;
  }
  .secondary {
    padding-top: 0;
    padding: 0;
    align-items: center;
  }
}
</style>
