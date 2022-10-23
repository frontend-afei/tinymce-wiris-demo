<template>
  <div id="app">
    <editor
      api-key="x1vyup3vl25v8l18tt7a9fx5efi78ldg0x8crp5j8m63v9r5"
      :init="init"
      :value="content"
      @input="onInput"
    />
  </div>
</template>

<script>
import Editor from "@tinymce/tinymce-vue";

export default {
  name: "app",
  components: {
    editor: Editor,
  },
  data() {
    return {
      content: '',
      init: {
        height: 500,
        menubar: false,
        language: "zh_CN",
        plugins: [
          "advlist autolink lists link image charmap print preview anchor",
          "searchreplace visualblocks code fullscreen",
          "insertdatetime media table paste code help wordcount",
          "emoticons",
        ],
        toolbar:
          "undo redo | formatselect | bold italic backcolor | \
          alignleft aligncenter alignright alignjustify | \
          bullist numlist outdent indent | removeformat | help | \
          emoticons image media | \
          kityformula-editor tiny_mce_wiris_formulaEditor tiny_mce_wiris_formulaEditorChemistry",
        external_plugins: {
          "kityformula-editor":"/tinymce/plugins/kityformula-editor/plugin.min.js", // 百度的数学公式
          "tiny_mce_wiris": `/tinymce/plugins/@wiris/mathtype-tinymce5/plugin.min.js`, // wiris的数学公式、化学公式
        },
        htmlAllowedTags: [".*"],
        htmlAllowedAttrs: [".*"],
        draggable_modal: true,
        // 自定义文件选择器的回调内容
        file_picker_callback: function (callback, value, meta) {
          if (meta.filetype == "image") {
            // ... 上传图片，拿到图片的 url ，假设为 myImage.jpg
            callback("myImage.jpg", { alt: "My alt text" });
          }
          if (meta.filetype == "media") {
            // ... 上传视频，拿到视频的 url ，假设为 myImage.mp4
            // source2 为备用地址，poster 为封面
            callback("myMovie.mp4", { source2: "alt.ogg", poster: "image.jpg" });
          }
        },
      },
    };
  },
  methods: {
    onInput(content) {
      console.log(content)
    }
  },
};
</script>
