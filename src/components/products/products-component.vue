<template>
  <div class="product-container">
    <table class="text-left" id="table">
      <thead>
      <tr>
        <th v-for="item in thead" :key="item" class="p-3">{{ item }}</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="item in products" :key="item" class="table-row">
        <td>{{ item.title }}</td>
        <td>{{ item.category }}</td>
        <td>{{ item.brand }}</td>
        <td>{{ new Intl.NumberFormat().format(+item.price) }}</td>
        <td>{{ item.discountPercentage }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  props: {
    products: Array
  },
  mounted() {
  },
  data() {
    return {
      thead: [
        'name',
        'category',
        'brand',
        'price',
        'discount(%)'
      ]
    }
  }
}
</script>
<style lang="scss" scoped>
@import "style/products.scss";
</style>