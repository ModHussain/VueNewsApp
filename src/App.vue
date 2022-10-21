<script setup>
import NewsHeader from './components/NewsHeader.vue'
import NewsViewData from './components/NewsSideBar.vue'

</script>

<template>
      <NewsHeader msg="Vue News App" />
      <NewsViewData></NewsViewData>  
</template>

<style>
.content-view{
  float: left;
}
</style>
