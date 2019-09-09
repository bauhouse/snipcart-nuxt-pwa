<template>
  <div class="single-post">
    <h1>{{ attributes.title }}</h1>
    <p>{{ attributes.date }}</p>
    <span v-html="html" class="markdown"></span>
    <div class="products">
      <article v-for="(product, index) in attributes.products" :key="index">
        <img :src="`../${product.image}`" :alt="product.name" />
        <button
          class="buy-button snipcart-add-item"
          :data-item-id="product.sku"
          :data-item-name="product.name"
          :data-item-price="product.price"
          :data-item-image="product.image"
          :data-item-url="`https://snipcart-nuxt-pwa.netlify.com${currentUrl}`"
          >{{`$${product.price}`}}</button>
        <p class="product-name">{{product.name}}</p>
      </article>
    </div>
    <Bio />
  </div>
</template>

<script>
import Bio from "~/components/Bio";

export default {
  components: {
    Bio,
  },
  layout: "article",
  async asyncData({ params, route }) {
    const articleName = params.slug
    const markdownContent = await import(`~/contents/journal/${articleName}.md`)
    return {
      attributes: markdownContent.attributes,
      html: markdownContent.html,
      currentUrl: route.path
    };
  },
  head() {
    return {
      title: `${this.attributes.title} | Nuxt.js PWA store`
    }
  }
};
</script>
