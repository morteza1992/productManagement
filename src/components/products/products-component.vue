<template>
  <div class="product-container">
    <table class="text-left" id="table">
      <thead>
      <tr>
        <th v-for="item in thead" :key="item"
            :class="item === 'brand' || item === 'discount(%)'? 'hidden sm:table-cell':''"
            class="p-3">{{ item }}
        </th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="item in products" :key="item" class="table-row">
        <td>
          <img :src="item.thumbnail" style="width: auto; height: 40px" alt="">
        </td>
        <td>{{ item.title }}</td>
        <td>{{ item.category }}</td>
        <td class="hidden sm:table-cell">{{ item.brand }}</td>
        <td>{{ new Intl.NumberFormat().format(+item.price) }}</td>
        <td class="hidden sm:table-cell">{{ item.discountPercentage }}</td>
        <td>
          <i class="fas fa-edit mr-1" @click="$emit('update', item)"></i>
          <i class="fas fa-trash-alt" @click="$emit('deleteItem', item.id)"></i>
        </td>
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
        '',
        'name',
        'category',
        'brand',
        'price',
        'discount(%)',
        ''
      ]
    }
  }
}
</script>
<style lang="scss" scoped>
@import "style/products.scss";
</style>