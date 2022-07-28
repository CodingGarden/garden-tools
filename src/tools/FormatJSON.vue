<template>
  <div v-if="error" class="alert alert-danger">
    {{error}}
  </div>
  <form @submit.prevent="formatJSON(options.tabSize)">
    <fieldset>
      <div class="form-group">
        <label for="tabSize" class="form-label mt-4">Tab Size</label>
        <input v-model="options.tabSize" class="form-control" type="number" min="1" id="tabSize">
      </div>
      <button type="submit" class="btn btn-primary">Format</button>
      <button @click="formatJSON(0)" type="button" class="btn btn-primary">Minify</button>
      <button @click="clear" type="button" class="btn btn-danger right">Clear</button>
    </fieldset>
  </form>
  <div class="editor" ref="editor"></div>
</template>

<script setup>
import { ref, onMounted, reactive } from 'vue';
import * as monaco from 'monaco-editor/esm/vs/editor/editor.api';

const error = ref('');
const editor = ref(null);
const options = reactive({
  tabSize: 2,
});

let codeEditor;

onMounted(() => {
  codeEditor = monaco.editor.create(editor.value, {
    value: '',
    language: 'json',
    theme: 'vs-dark',
    fontSize: '24px',
  });
});

function clear() {
  if (!codeEditor) return;

  codeEditor.setValue('');
}

function formatJSON(tabSize) {
  if (!codeEditor) return;
  try {
    const jsonText = codeEditor.getValue();

    const formattedJSON = JSON.stringify(
      JSON.parse(jsonText),
      null,
      tabSize,
    );
    codeEditor.setValue(formattedJSON);
    codeEditor.setScrollLeft(0);
    error.value = '';
  } catch (e) {
    error.value = e.message;
  }
}
</script>

<style scoped>
form {
  width: 90%;
  margin: 2rem;
}

form input {
  margin: 1rem 0;
}

button {
  margin: 0 0.25rem;
}
.editor {
  height: 60vw;
  width: 90%;
}
.right {
  float: right;
}
</style>
