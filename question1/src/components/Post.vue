<template>
  <div class="d-flex post-container">
    <img :src="value.thumbnail" class="thumbnail" />
    <div class="d-flex flex-column justify-content-between" style="padding: 0 12px">
      <span class="title">{{value.title}}</span>
      <span class="price">{{value.formattedPrice}}</span>
      <div>
        <span class="content">Diện tích: <span class="area">{{value.formattedArea}}</span></span>
        <span class="content" style="margin-left: 16px">Khu vực: <span class="address">{{value.formattedAddress}}</span></span>
      </div>
      <span class="content">{{value.content}}...</span>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Post',
  props: ['value'],

}
</script>

<style scoped>
 .post-container {
   border: 1px solid red;
   background-color: peachpuff;
   padding: 8px 16px;
   max-width: 700px;
   text-align: left;
 }

 .thumbnail {
   width: 200px;
   height: 200px;
 }

 .title {
   color: red;
   font-size: 1.2rem;
 }

 .price {
    color: green;
    font-weight: bold;
    font-size: 1.3rem;
 }

 .content {
   color: grey;
 }

 .area {
   font-weight: bold;
 }

 .address {
   font-weight: bold;
   color: royalblue;
 }
</style>