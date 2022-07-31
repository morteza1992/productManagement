<template>
  <Layout-component>
    <products-component/>
    <form-component/>
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
  }
}
</script>

<style>
</style>
