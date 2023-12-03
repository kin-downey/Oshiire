<template>
  <editor-content :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import Link from '@tiptap/extension-link'
import Placeholder from '@tiptap/extension-placeholder'
import Mention from '@tiptap/extension-mention'
import suggestion from './suggestion.js'

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
        Mention.configure({
          HTMLAttributes: {
            class: 'mention',
          },
          suggestion,
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

.mention {
  border: 1px solid #000;
  border-radius: 0.4rem;
  padding: 0.1rem 0.3rem;
  box-decoration-break: clone;
}
</style>