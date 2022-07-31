<template>
  <div class="form-container">
    <div class="row text-lg font-bold text-purple-800 pb-3">
      Create a New Product
    </div>
    <div class="flex justify-center items-start">
      <form class="left-section">

        <div class="row">
          <label>Product Name</label>
          <input class="input" v-model="title"/>
        </div>
        <div class="row">
          <label>Price</label>
          <input class="input" v-model="price" type="number"/>
        </div>
        <div class="row">
          <label>Category</label>
          <select>
            <option></option>
          </select>
        </div>
        <div class="row">
          <label>Brand</label>
          <select>
            <option></option>
          </select>
        </div>
        <div class="row">
          <label>Description</label>
          <textarea rows="5"></textarea>
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
        <div class="button-container">
          <button class="border py-1 px-3" type="button">Clear</button>
          <button class="border py-1 px-3 bg-blue-800 text-white" type="button">Submit</button>
        </div>
      </div>
    </div>

  </div>

</template>
<style lang="scss" scoped>
@import "style/form.scss";
</style>