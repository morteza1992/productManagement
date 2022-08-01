<template>
  <Layout-component>
    <products-component :products="products"/>
    <form-component :categoriesList="categoriesList"/>
  </Layout-component>
</template>

<script>
import LayoutComponent from "@/components/layout/layout-component.vue";
import productsComponent from "@/components/products/products-component.vue";
import formComponent from "@/components/form/form-component.vue";


export default {
  name: 'product-management',
  components: {
    LayoutComponent,
    productsComponent,
    formComponent
  },
  data() {
    return {
      categoriesList: [],
      products: []
    }
  },
  mounted() {
    this.getCategoriesList()
    this.getProducts()
  },
  methods: {
    sendRequest: async function (URL, method) {
      let requestOptions = {
        method: method,
        redirect: 'follow'
      };
      const finalUrl = "https://dummyjson.com/products" + URL
      return await new Promise((resolve, reject) => {
        fetch(finalUrl, requestOptions)
            .then(response => response.json())
            .then(response => {
              resolve(response)
            })
            .catch(error => {
              reject(error)
            });
      })
    },
    getProducts: async function () {
      try {
        let products = await this.sendRequest('', 'GET')
        this.products = products.products
      } catch (error) {
        alert(error)
      }
    },
    getCategoriesList: async function () {
      try {
        this.categoriesList = await this.sendRequest('/categories', 'GET')
      } catch (error) {
        alert(error)
      }
    }
  }
}
</script>
<style>
</style>
