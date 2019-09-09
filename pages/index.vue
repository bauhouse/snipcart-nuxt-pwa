<template>
  <div class="main">
    <main>
      <div>
        <article class="post" v-for="(article, index) in articles" :key="index">
          <div class="post-aside">
            <small>{{ article.attributes.date }}</small>
            <h3 class="post-title"><nuxt-link :to="article.attributes.link">{{ article.attributes.title }}</nuxt-link></h3>
            <p>{{ article.attributes.description }}</p>
          </div>
          <div class="products">
            <article v-for="(product, index) in article.attributes.products" :key="index">
              <img :src="product.image" :alt="product.name">
              <button
                class="buy-button snipcart-add-item"
                :data-item-id="product.sku"
                :data-item-name="product.name"
                :data-item-price="product.price"
                :data-item-image="product.image"
                :data-item-url="`https://snipcart-nuxt-pwa.netlify.com/`">
                {{`$${product.price}`}}
              </button>
              <p class="product-name">{{product.name}}</p>
            </article>
          </div>
        </article>
      </div>
      <Testimonals />
    </main>
  </div>
</template>

<script>
import articles from '~/contents/journal/articles.js'

export default {
  async asyncData ({ route }) {
    const promises = articles.map(article => import(`~/contents/journal/${article}.md`))
    return { articles: await Promise.all(promises) }
  },
  head() {
    return {
      title: "All posts | Nuxt.js PWA store"
    }
  }
}
</script>
