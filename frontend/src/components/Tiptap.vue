<template>
  <editor-content :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import Link from '@tiptap/extension-link'
import Placeholder from '@tiptap/extension-placeholder'

export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      editor: null,
    }
  },

  mounted() {
    this.editor = new Editor({
      content: '',
      extensions: [
        StarterKit,
        Link.configure({
          openOnClick: true,
          validate: href => /^http?:\/\//.test(href),
        }),
        Placeholder.configure({
          placeholder: 'Write something …',
        }),
      ],
    })
  },

  beforeUnmount() {
    alert('beforeUnmount')
    this.editor.destroy()
  },
}
</script>

<style>
/* Basic editor styles */
.tiptap {
  > * + * {
    margin-top: 0.75em;
  }
}

/* Placeholder (at the top) */
.tiptap p.is-editor-empty:first-child::before {
  content: attr(data-placeholder);
  float: left;
  color: #adb5bd;
  pointer-events: none;
  height: 0;
}

/* Placeholder (on every new line) */
/*.tiptap p.is-empty::before {
  content: attr(data-placeholder);
  float: left;
  color: #adb5bd;
  pointer-events: none;
  height: 0;
}*/
</style>