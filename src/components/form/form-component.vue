<template>
  <div class="form-container">
    <div class="row text-lg font-bold text-purple-800 pb-3">
      {{ actionType !== 'update' ? 'Create a New Product' : 'Update Product' }}
    </div>
    <div class="flex justify-center items-start">
      <form class="left-section">

        <div class="row">
          <label>Product Name</label>
          <input class="input" v-model="title" :class="!title && errorText? 'border-red':''"/>
        </div>
        <div class="row">
          <label>Price</label>
          <input class="input" v-model="price" type="number"/>
        </div>
        <div class="row">
          <label>Category</label>
          <select v-model="Category">
            <option v-for="(item, index) in categoriesList" :value="item" :key="index">{{ item }}</option>
          </select>
        </div>
        <div class="row">
          <label>Brand</label>
          <select v-model="Brand">
            <option>Apple</option>
            <option>Sony</option>
            <option>samsung</option>
          </select>
        </div>
        <div class="row">
          <label>Description</label>
          <textarea rows="5" v-model="Description"></textarea>
          <div class="text-xs">do not exceed 100 characters</div>
        </div>
      </form>
      <div class="right-section">
        <div class="file-container">
          <div>
            <input class="hidden" type="file" id="file"/>
            <label for="file" class="file">
              <i class="fas fa-image text-2xl mb-2"></i>
              <span>Drop your image here, or select </span>
              <span class="text-purple-800">click to brows</span>
            </label>
          </div>
        </div>
        <div>{{ errorText }}</div>
        <div class="button-container">
          <button class="border py-1 px-3" type="button">Clear</button>
          <button @click="returnFormData" class="border py-1 px-3 bg-blue-800 text-white" type="button">
            {{ actionType !== 'update' ? 'Submit' : 'Update' }}
          </button>
        </div>
      </div>
    </div>

  </div>

</template>
<script>
export default {
  props: {
    categoriesList: Array,
    actionType: String
  },
  data() {
    return {
      title: null,
      price: null,
      Category: null,
      Brand: null,
      Description: null,
      errorText: null
    }
  },
  methods: {
    returnFormData: function () {
      let body = {
        title: this.title,
        price: this.price,
        Category: this.Category,
        Brand: this.Category,
        Description: this.Description
      }
      if (this.title) {
        this.$emit('formData', body)
      } else {
        this.errorText = 'please fill the name'
      }

    },
    fillData: function (data) {
      console.log(data)
      this.title = data.title
      this.price = data.price
      this.Category = data.category
      this.Brand = data.brand
      this.Description = data.description
      this.errorText = data.errorText
    },
    resetData: function () {
      this.title = null
      this.price = null
      this.Category = null
      this.Brand = null
      this.Description = null
      this.errorText = null
    }
  }
}
</script>
<style lang="scss" scoped>
@import "style/form.scss";
</style>