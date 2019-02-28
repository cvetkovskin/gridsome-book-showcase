<template>
  <Layout>
    <div class="books">
      <div class="book" v-for="book in $page.allBookEntry.edges" :key="book.node.id">
        <h2>
          <g-link :to="`showcase/${book.node.id}`">{{ book.node.title }}</g-link>
        </h2>

        <div class="content">
          <div class="img-wrapper">
            <g-image  :src="book.node.cover.medium" />
          </div>

          <div>{{ shortenText(book.node.byStatement) }}</div>
        </div>

        <div class="book-footer">
          <div>{{ book.node.publishDate }}</div>
          <div>By <span v-html="book.node.authors[0].name" /></div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query {
  allBookEntry {
    edges {
      node{
        id
        title
        authors {
					name
        },
        cover {
          medium
        }
        byStatement
        publishDate
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: 'Showcase'
  },

  methods: {
    shortenText(text) {
      return text.slice(0,300) + '...'
    }
  }
}
</script>

<style scoped>
.books {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.book {
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.1);
  padding: 0 15px 20px;
  margin: 20px 5px;
  width: 300px;
}

.img-wrapper {
  width: 100%;
  text-align: center;
}

.img-wrapper img {
  height: 200px;
}

.book-footer {
  margin-top: 30px;
  display: flex;
  justify-content: space-between;
}
</style>
