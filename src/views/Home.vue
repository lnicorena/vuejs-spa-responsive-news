<template>
  <div>
    <Navbar :categories="categories" @categorySelected="filterArticles" />
    <div class="main-container" v-if="loaded">
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
    <div class="main-container loader" v-else></div>
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
      loaded: false,
      articlesList: {
        data: [],
        itemsPage: 6,
        currentPage: 0,
        totalPages: 0,
        totalItems: 0
      },
      categories: [],
      categoryFilter: 0
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
      return this.articlesList.data.length == 0
        ? []
        : this.articlesList.data[0];
    },
    featuredArticles() {
      if (this.articlesList.data.length < 2) return [];
      else
        return this.articlesList.data.length == 2
          ? [this.articlesList.data[1]]
          : this.articlesList.data.slice(1, 3);
    },
    defaultArticles() {
      if (this.articlesList.data.length < 4) return [];
      else
        return this.articlesList.data.slice(3, this.articlesList.data.length);
    }
  },
  methods: {
    loadCategories() {
      this.$api.get("/categories").then(res => {
        if (res.statusText == "OK" && res.data.length) {
          this.categories = res.data;
        }
      });
    },
    filterArticles(id) {
      this.categoryFilter = id;
      this.loadArticles();
    },
    loadArticles() {
      this.loaded = false;

      this.$api
        .get("/articles", {
          params: {
            page: this.articlesList.currentPage + 1,
            category: this.categoryFilter
          }
        })
        .then(res => {
          if (res.statusText == "OK" && res.data.data.length) {
            /* @todo load more articles button */

            this.articlesList.totalItems = res.data.total;
            this.articlesList.itemsPage = res.data.per_page;
            this.articlesList.currentPage = res.data.current_page;
            this.articlesList.totalPages = res.data.last_page;
            this.articlesList.data = res.data.data;
            this.loaded = true;
          }
        });
    }
  }
};
</script>

<style>
.main-container {
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

.main-container.loader {
  background-image: url("~@/assets/loading.gif");
  background-position: center center;
  background-repeat: no-repeat;
  position: absolute;
  margin: auto;
  background-size: 32px;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
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
  min-height: 525px;
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
  padding-top: 2em;
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
