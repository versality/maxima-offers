<template>
<div class="mdl-grid">
  <div v-for="product in products" class="mdl-cell mdl-cell--3-col">
    <div class="mdl-card mdl-shadow--4dp">
      <div class="mdl-card__media">
        <img v-bind:src="'https://beta.e-maxima.lv' + product.SmallImageUrl" height="100%" style="padding: 10px">
      </div>

      <div class="mdl-card__supporting-text mdl-card--border">
        {{ product.Price.Price }}
      </div>

      <div class="mdl-card__supporting-text mdl-card--border">
        {{ product.Name }}
      </div>
    </div>
  </div>
</div>
</template>

<style>
  .mdl-card {
    width: 260px;
  }

  .mdl-card__media {
    background-color: white;
    
  }

  .mdl-card__media > img {
    display: block;
    margin: 0 auto;
  }
</style>

<script>
  export default {
    data: function () {
      return {
        products: '',
        error: {}
      }
    },

    mounted() {
      this.fetchProducts()
    },

    methods: {
      fetchProducts() {
        this.$http.get('/api/proxy').then((response) => {
          this.products = JSON.parse(response.data)
        }, (response) => {
          this.error = JSON.stringify(response.data)
        })
      }
    }
  }
</script>