<script setup>
import { useRoute } from "vue-router";
import { data, fn } from "../../data.js";
import { ref, watch } from "vue";

const route = useRoute();
const postDetails = ref({});

const getPostDetails = () => {
  const res = fn.fetchPublicApi(`/posts/${route.params.id}`, "get");
  res.then((response) => {
    postDetails.value = response;
  });
};

getPostDetails();

// watch(route, () => {
//   getPostDetails();
// });

</script>
<template>

  <!-- <h2>Related Posts</h2>
  <router-link class="block text-xl mt-4 lg:inline-block lg:mt-0 text-black mr-10" to="/blog/1">Blog 1</router-link>
  <router-link class="block text-xl mt-4 lg:inline-block lg:mt-0 text-black" to="/blog/2">Blog 2</router-link> -->

  <div class="mx-auto w-[700px] rounded overflow-hidden shadow-lg">
    <img
        class="w-full"
        src="https://v1.tailwindcss.com/img/card-top.jpg"
        alt="Sunset in the mountains"
    />
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">
        {{ postDetails.title }}
      </div>
      <p class="text-gray-700 text-base">{{ postDetails.body }}</p>
    </div>
    <div class="px-6 pt-4 pb-2">
      <span
          v-for="tag in postDetails.tags"
          :key="tag"
          class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
      >#{{ tag }}</span
      >
    </div>
  </div>
</template>