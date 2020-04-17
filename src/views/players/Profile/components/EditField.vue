<template>
  <div>
    <!-- Use the component in the right place of the template -->
    <tiptap-vuetify v-model="content" :extensions="extensions" />
  </div>
</template>

<script lang="ts">
  import { Component, Vue, Mixins } from 'vue-property-decorator';
  // @ts-ignore
  import {
    TiptapVuetify,
    Heading,
    Bold,
    Italic,
    Strike,
    Underline,
    Code,
    Paragraph,
    BulletList,
    OrderedList,
    ListItem,
    Link,
    Blockquote,
    HardBreak,
    HorizontalRule,
    History,
  } from 'tiptap-vuetify';

  @Component({
    components: { TiptapVuetify },
  })
  export default class EditField extends Vue {
    private extensions = [
      History,
      Blockquote,
      Link,
      Underline,
      Strike,
      Italic,
      ListItem,
      BulletList,
      OrderedList,
      [
        Heading,
        {
          options: {
            levels: [1, 2, 3],
          },
        },
      ],
      Bold,
      Code,
      HorizontalRule,
      Paragraph,
      HardBreak,
    ];

    // starting editor's content
    private content = `
      <h1>Yay Headlines!</h1>
      <p>All these <strong>cool tags</strong> are working now.</p>
    `;
  }
</script>
<style lang="scss" scoped>
  // don't forget to import CSS styles
  @import '~tiptap-vuetify/dist/main.css';
  // Vuetify's CSS styles
  @import '~vuetify/dist/vuetify.min.css';

  .editor-box > * {
    border-color: grey;
    border-style: solid;
    border-width: 1px;
  }

  .is-active {
    border-color: grey;
    border-style: solid;
    border-width: 1px;
  }
  /* *:focus {
      outline: none;
  }  */
</style>
