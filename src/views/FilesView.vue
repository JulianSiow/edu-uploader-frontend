<template>
  <div>
    <h1>Files</h1>
    <ul class="file-list">
      <FileItem v-for="file in files" :key="file" :fileName="file" />
    </ul>
    <h2 v-if="files && files.length < 1">
      There seem to be no files here! Please upload a file
    </h2>
  </div>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
import FileItem from "@/components/FileItem.vue";

export default {
  components: {
    FileItem,
  },

  setup() {
    const files = ref(null);

    const getFiles = () => {
      axios
        .get(`${process.env.VUE_APP_API_PORT}/files`)
        .then((res) => {
          files.value = res.data.data;
        })
        .catch((err) => {
          console.log(err);
        });
    };

    onMounted(() => {
      getFiles();
    });

    return {
      files,
      getFiles,
    };
  },
};
</script>

<style>
.file-list {
  list-style-type: none;
  margin: 0 auto;
  max-width: 50%;
  padding-left: 0px;
}
.file:not(:first-child) {
  border-top: 1px solid #2c3e50;
}
</style>
