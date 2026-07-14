<script setup>
import { ref, computed, onMounted } from 'vue';

const props = defineProps({
  options: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['close']);

const copied = ref(false);

const jsonString = computed(() => JSON.stringify(props.options, null, 2));

const handleCopy = () => {
  navigator.clipboard.writeText(jsonString.value).then(() => {
    copied.value = true;
    setTimeout(() => {
      copied.value = false;
    }, 2000);
  });
};

const highlightedCode = computed(() => {
  return jsonString.value
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|-?\d+(?:\.\d*)?(?:[eE][+\-]?\d+)?)/g, (match) => {
      let cls = 'number';
      if (/^"/.test(match)) {
        if (/:$/.test(match)) {
          cls = 'key';
        } else {
          cls = 'string';
        }
      } else if (/true|false/.test(match)) {
        cls = 'boolean';
      } else if (/null/.test(match)) {
        cls = 'null';
      }
      return `<span class="code-${cls}">${match}</span>`;
    });
});
</script>

<template>
  <div class="code-viewer-overlay" @click="$emit('close')">
    <div class="code-viewer-content" @click.stop>
      <button class="close-btn" @click="$emit('close')">
        &times;
      </button>
      <button class="copy-btn" @click="handleCopy">
        {{ copied ? 'Copied!' : 'Copy' }}
      </button>
      <h3 class="code-viewer-title">
        Chart Options
      </h3>
      <pre class="code-viewer-pre"><code v-html="highlightedCode"></code></pre>
    </div>
  </div>
</template>

<style scoped>
.code-viewer-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.code-viewer-content {
  background-color: #ffffff;
  color: #333333;
  padding: 30px 20px 20px 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 800px;
  max-height: 80%;
  overflow: auto;
  position: relative;
  box-shadow: 0 10px 40px rgba(0,0,0,0.2);
  border: 1px solid #ddd;
}

.close-btn {
  position: absolute;
  top: 5px;
  right: 10px;
  background: transparent;
  border: none;
  color: #999;
  fontSize: 24px;
  cursor: pointer;
  lineHeight: 1;
}

.copy-btn {
  position: absolute;
  top: 10px;
  right: 40px;
  background: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 8px;
  font-size: 12px;
  cursor: pointer;
  color: #333;
}

.code-viewer-title {
  margin-top: 0;
  margin-bottom: 15px;
  color: #0066cc;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
}

.code-viewer-pre {
  margin: 0;
  font-family: monospace;
  font-size: 13px;
  line-height: 1.5;
}

:deep(.code-key) { color: #a31515; font-weight: bold; }
:deep(.code-string) { color: #0451a5; }
:deep(.code-number) { color: #098658; }
:deep(.code-boolean) { color: #0000ff; }
:deep(.code-null) { color: #0000ff; }
</style>
