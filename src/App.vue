<template>
  <div v-if="loading" class="loading">LOADING ...</div>
  <div v-if="modal" class="loading">
    <div class="modal-content">
      <div>the selected row will be delete</div>
      <div class="flex items-center justify-center">
        <button @click="deleteConfirm">confirm</button>
        <button @click="modal = false">cancel</button>
      </div>
    </div>
  </div>
  <Layout-component>
    <form-component
        @formData="formData"
        ref="form"
        :actionType="actionType"
        :categoriesList="categoriesList"/>
    <products-component
        @update="update"
        @deleteItem="deleteItem"
        :products="products"/>
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
      products: [],
      itemId: null,
      actionType: null,
      loading: false,
      modal: false
    }
  },
  mounted() {
    this.getCategoriesList()
    this.getProducts()
  },
  methods: {
    sendRequest: async function (URL, method, body) {
      this.loading = true
      let requestOptions = {
        method: method,
        redirect: 'follow'
      };
      if (body) {
        requestOptions['body'] = JSON.stringify(body)
        requestOptions['Content-Type'] = 'application/json'
      }
      console.log(requestOptions)
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
      } finally {
        this.loading = false
      }
    },
    getCategoriesList: async function () {
      try {
        this.categoriesList = await this.sendRequest('/categories', 'GET')
      } catch (error) {
        alert(error)
      }
    },
    formData: async function (value) {
      let URL = '/add'
      let method = 'POST'
      if (this.actionType === 'update') {
        URL = '/' + this.itemId
        method = 'PUT'
      }
      try {
        await this.sendRequest(URL, method, value)
        this.actionType = null
        this.$refs.form.resetData()
      } catch (error) {
        alert(error)
      } finally {
        this.loading = false
      }
    },
    update: function (value) {
      this.actionType = 'update'
      this.itemId = value.id
      this.$refs.form.fillData(value)
    },
    deleteItem: function (value) {
      this.itemId = value
      this.modal = true
    },
    deleteConfirm: async function () {
      this.modal = false
      try {
        let URL = '/' + this.itemId
        await this.sendRequest(URL, 'DELETE')
      } catch (error) {
        alert(error)
      } finally {
        this.loading = false
      }
    }
  }
}
</script>
<style>
</style>
