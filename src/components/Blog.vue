<script setup>
import { data, fn } from "../data.js";

const getPosts = () => {
  const res = fn.fetchPublicApi("/posts", "get");
  res.then((response) => {
    data.posts = response.posts;
  });
};
getPosts();

</script>
<template>
  <router-view></router-view>
</template>