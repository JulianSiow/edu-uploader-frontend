<template>
  <li class="file">
    {{ fileName }}
    <button @click="downloadFile">Download File</button>
  </li>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";

export default defineComponent({
  props: {
    fileName: String,
  },

  setup(props) {
    const downloadFile = () => {
      axios
        .get(`${process.env.VUE_APP_API_PORT}/files/${props.fileName}`)
        .then((res) => {
          console.log(res);
          var fileURL = window.URL.createObjectURL(new Blob([res.data]));
          var fileLink = document.createElement("a");

          fileLink.href = fileURL;
          fileLink.setAttribute("download", props.fileName);
          document.body.appendChild(fileLink);

          fileLink.click();
        })
        .catch((err) => {
          console.log(err);
        });
    };

    return {
      downloadFile,
    };
  },
});
</script>

<style>
.file {
  padding: 10px;
  display: flex;
  justify-content: space-between;
}
</style>
