<template>
  <div :class="className">
    <AuthorImage
      class="photo"
      :url="authorPhoto"
      noimage="user"
      :loader="true"
    />
    <p class="name">{{ authorName }}</p>
  </div>
</template>

<script>
import AuthorImage from "@/components/_image.vue";
export default {
  components: { AuthorImage },
  data() {
    return {
      showAuthorsMax: 1
    };
  },
  props: {
    authors: Array,
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
    authorPhoto() {
      return this.authors.length == 0 ? "" : this.authors[0].avatar;
    },
    authorName() {
      if (this.authors.length == 0) return "Unkown";
      else
        return this.filteredAuthors
          .map(a => {
            return a.name;
          })
          .join(", ");
    },
    filteredAuthors() {
      let max =
        this.authors.length <= this.showAuthorsMax
          ? this.authors.length
          : this.showAuthorsMax;
      return this.authors.slice(0, max);
    },
    className() {
      return `article-author-${this.mode}`;
    }
  }
};
</script>

<style scoped>
.article-author-default,
.article-author-featured,
.article-author-headline {
  margin: 15px 0px 20px 0px;
  font-size: 13px;
  font-family: "Open Sans", sans-serif;
  display: flex;
  transition-property: all;
  transition-duration: 0.5s;
  color: #808080;
  font-style: italic;
}

.photo {
  margin-top: 5px;
  border-radius: 100px;
  margin-right: 0.5em;
  font-weight: bold;

  width: 45px;
  height: 45px;
}
@media (max-width: 750px) {
  .photo {
    height: 32px;
    width: 32px;
  }
}

.name {
  text-align: center;
  margin-top: 20px;
}
.article-author-default .name,
.article-author-headline .name {
  margin-bottom: 0;
}
@media (max-width: 750px) {
  .name {
    margin-bottom: 13px;
    margin-top: 13px;
  }
}
</style>
