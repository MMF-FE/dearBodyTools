<script>
import { defineComponent, ref, reactive, watch } from "vue";
import { QuillEditor } from "@vueup/vue-quill";
import "@vueup/vue-quill/dist/vue-quill.snow.css";

export default defineComponent({
  components: {
    QuillEditor,
  },

  props: {
    value: String,
  },
  setup(props, { emit }) {
    const quillEditor = ref();
    const myContent = ref(props.value);
    const options = reactive({
      modules: {
        toolbar: [
          ["bold", "italic", "underline", "strike"], // toggled buttons
          ["blockquote", "code-block"],

          [{ header: 1 }, { header: 2 }], // custom button values
          [{ list: "ordered" }, { list: "bullet" }],
          [{ script: "sub" }, { script: "super" }], // superscript/subscript
          [{ indent: "-1" }, { indent: "+1" }], // outdent/indent
          [{ direction: "rtl" }], // text direction

          [{ size: ["small", false, "large", "huge"] }], // custom dropdown
          [{ header: [1, 2, 3, 4, 5, 6, false] }],

          [{ color: [] }, { background: [] }], // dropdown with defaults from theme
          [{ font: [] }],
          [{ align: [] }],
          ["clean"],
          ["image"],
        ],
      },
      theme: "snow",
      placeholder: "输入您喜欢的内容吧！",
    });
    const readyQuill = () => {
      console.log(props.value);
      quillEditor.value.setHTML(props.value);
    };
    watch(
      () => myContent.value,
      () => {
        if (quillEditor.value) {
          const value = quillEditor.value.getHTML();
          emit("update:value", value);
        }
      },
      {
        immediate: true,
        deep: true,
      }
    );
    return {
      quillEditor,
      options,
      myContent,
      readyQuill,
    };
  },
});
</script>

<template>
  <QuillEditor
    ref="quillEditor"
    theme="snow"
    v-model:content="myContent"
    style="height: 350px"
    @ready="readyQuill"
    class="quillEditor"
  />
</template>
