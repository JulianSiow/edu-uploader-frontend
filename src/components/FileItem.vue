<template>
  <li>
    {{ fileName }}
    <button @click="downloadFile">Download File</button>
  </li>
</template>

<script>
import { defineComponent } from "vue";
import axios from "axios";

export default defineComponent({
  props: {
    fileName: String,
  },

  setup(props) {
    const downloadFile = () => {
      axios
        .get(`http://localhost:8080/files/${props.fileName}`)
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

<style></style>
