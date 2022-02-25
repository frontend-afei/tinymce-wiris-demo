<template>
  <div id="app">
    <editor
      api-key="x1vyup3vl25v8l18tt7a9fx5efi78ldg0x8crp5j8m63v9r5"
      :init="init"
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
          "kityformula-editor":"/tinymce/plugins/kityformula-editor/plugin.min.js", // 百度数学公式
          "tiny_mce_wiris": `/tinymce/plugins/@wiris/mathtype-tinymce5/plugin.min.js`, // wiris 数学公式、化学公式
        },
        htmlAllowedTags: [".*"],
        htmlAllowedAttrs: [".*"],
        draggable_modal: true,
        //自定义文件选择器的回调内容
        file_picker_callback: function (callback, value, meta) {
          // Provide file and text for the link dialog
          if (meta.filetype == "file") {
            callback("mypage.html", { text: "My text" });
          }

          // Provide image and alt text for the image dialog
          if (meta.filetype == "image") {
            callback("myimage.jpg", { alt: "My alt text" });
          }

          // Provide alternative source and posted for the media dialog
          if (meta.filetype == "media") {
            callback("movie.mp4", { source2: "alt.ogg", poster: "image.jpg" });
          }
        },
      },
    };
  },
};
</script>
