<script>
import { defineComponent, nextTick, onMounted, reactive, ref } from "vue";
import {
  NConfigProvider,
  NForm,
  NFormItem,
  NInput,
  NButton,
  NSpace,
  NCard,
  darkTheme,
  useNotification,
  NPopconfirm,
  NScrollbar,
} from "naive-ui";
import hljs from "highlight.js/lib/core";
import json from "highlight.js/lib/languages/json";
hljs.registerLanguage("json", json);
import Editor from "./QuillEditor.vue";
import "@vueup/vue-quill/dist/vue-quill.snow.css";
export default defineComponent({
  components: {
    NConfigProvider,
    NButton,
    NForm,
    NFormItem,
    NInput,
    NSpace,
    NCard,
    NPopconfirm,
    Editor,
    NScrollbar,
  },
  setup() {
    const formRef = ref(null);
    const copyCode = ref("");
    const notification = useNotification();
    const loading = ref(false);
    const code = reactive({
      list: [{ title: "", content: "" }],
    });
    const removeItem = (index) => {
      code.list.splice(index, 1);
    };

    const addItem = () => {
      code.list.push({ title: "", content: "" });
    };

    const handleValidateClick = () => {
      formRef.value?.validate((errors) => {
        if (!errors) {
          console.log("验证通过");
          copyTextToClipboard();
        } else {
          console.log(errors);
          notification.error({
            title: "error",
            content: "Please enter the content in the red box",
            duration: 2500,
            keepAliveOnHover: true,
          });
        }
      });
    };
    const copyTextToClipboard = () => {
      const text = JSON.stringify(code);
      const input = document.createElement("input");
      document.body.appendChild(input);
      input.setAttribute("value", text);
      input.select();
      if (document.execCommand("copy")) {
        document.execCommand("copy");
        notification.success({
          title: "success",
          content: "Copy success",
          duration: 2500,
          keepAliveOnHover: true,
        });
      } else {
        console.error("复制失败");
      }
      document.body.removeChild(input);
    };
    const handlePositiveClick = async () => {
      loading.value = true;
      try {
        formRef.value.restoreValidation();
        const copy = JSON.parse(copyCode.value);
        code.list = copy.list;
        notification.success({
          title: "success",
          content: "Covered success",
          duration: 2500,
          keepAliveOnHover: true,
        });
      } catch (error) {
        console.log(error);
      }
      await nextTick();
      loading.value = false;
      copyCode.value = "";
    };
    onMounted(() => {});

    return {
      code,
      formRef,
      darkTheme,
      theme: ref(null),
      hljs,
      removeItem,
      addItem,
      handleValidateClick,
      copyTextToClipboard,
      copyCode,
      loading,
      handlePositiveClick,
    };
  },
});
</script>

<template>
  <n-config-provider :theme="theme" :hljs="hljs">
    <div class="flex-slider">
      <div class="slider-warp">
        <div class="actions">
          <div class="title">actions</div>
          <n-popconfirm @positive-click="handlePositiveClick">
            <template #trigger>
              <n-button attr-type="button" type="warning">
                Covered code
              </n-button>
            </template>
            <n-input
              class="input"
              v-model:value="copyCode"
              type="textarea"
              clearable
            />
          </n-popconfirm>
          <n-button
            attr-type="button"
            type="success"
            class="slider-left"
            @click="handleValidateClick"
          >
            copy code
          </n-button>
          <n-button
            class="slider-left"
            attr-type="button"
            type="info"
            @click="addItem"
          >
            add item
          </n-button>
        </div>
      </div>
      <n-scrollbar style="max-height: 100vh" trigger="none">
        <!-- <pre>{{ JSON.stringify(code, null, 2) }}</pre> -->
        <n-form ref="formRef" class="flex-warp" :model="code">
          <n-space class="form-warp" align="start">
            <template v-for="(item, index) in code.list" :key="index">
              <n-card
                :title="`content${index + 1}`"
                class="card"
                :segmented="{
                  content: true,
                  footer: 'soft',
                }"
              >
                <template #action>
                  <n-button
                    style="margin-left: 12px"
                    type="error"
                    @click="removeItem(index)"
                  >
                    delete
                  </n-button>
                </template>
                <n-form-item
                  :label="`Please enter title${index + 1}`"
                  :path="`list[${index}].title`"
                  :rule="{
                    required: true,
                    message: `Please enter title${index + 1}`,
                    trigger: ['input', 'blur'],
                  }"
                >
                  <n-input class="input" v-model:value="item.title" clearable />
                </n-form-item>
                <n-form-item
                  :label="`Please enter content${index + 1}`"
                  :path="`list[${index}].content`"
                  :rule="{
                    required: true,
                    message: `Please enter content${index + 1}`,
                    trigger: ['input', 'blur'],
                  }"
                >
                  <div class="input" v-if="!this.loading">
                    <Editor v-model:value="item.content" />
                  </div>
                </n-form-item>
              </n-card>
            </template>
          </n-space>
        </n-form>
      </n-scrollbar>
    </div>
  </n-config-provider>
</template>

<style>
.flex-warp {
  display: flex;
  justify-items: center;
  align-content: flex-start;
  flex-wrap: wrap;
}
.flex-copy-json {
  flex: 1;
  margin-right: 20px;
  text-align: left;
}
.dynamic-warp {
  width: 680px;
  margin: auto;
}
.input {
  width: 100%;
  text-align: left;
}
.card {
  width: 640px;
}
.card-actions {
  width: 640px;
  margin-bottom: 30px;
  display: flex;
  justify-content: space-between;
}
.flex-warp {
  margin-bottom: 60px;
}
.flex-slider {
  display: flex;
}
.slider-warp {
  background: #2c3e50;
  min-height: 100vh;
  height: 100%;
  display: flex;
}
.actions {
  display: flex;
  height: auto;
  flex-direction: column;
  padding: 10px;
  padding-top: 20px;
}
.title {
  color: #fff;
  font-weight: bold;
  font-size: 30px;
  text-align: center;
  padding-bottom: 40px;
}
.slider-left {
  margin-top: 30px;
}
</style>