<template>
  <n-config-provider>
    <n-message-provider>
      <main class="shell">
        <section class="hero">
          <p class="eyebrow">Todo</p>
          <h1>新的主线工程已初始化</h1>
          <p class="summary">
            当前阶段只验证三件事：Vue 骨架、Naive UI 日期控件、Tauri command 通路。
          </p>
        </section>

        <section class="panel-grid">
          <n-card title="日期控件验证" size="small" class="panel">
            <div class="field-stack">
              <label class="field-label">截止时间</label>
              <n-date-picker
                v-model:value="dueAt"
                type="datetime"
                clearable
                class="date-field"
              />
            </div>
          </n-card>

          <n-card title="Rust Command 验证" size="small" class="panel">
            <div class="field-stack">
              <label class="field-label" for="name">名字</label>
              <input id="name" v-model="name" class="text-input" />
              <button class="primary-button" type="button" @click="handleInvoke">
                调用 greet
              </button>
              <p class="result">{{ greetResult }}</p>
            </div>
          </n-card>
        </section>
      </main>
    </n-message-provider>
  </n-config-provider>
</template>

<script setup lang="ts">
import { invoke } from '@tauri-apps/api/core'
import { NCard, NConfigProvider, NDatePicker, NMessageProvider } from 'naive-ui'
import { ref } from 'vue'

const dueAt = ref<number | null>(null)
const greetResult = ref('尚未调用')
const name = ref('Todo')

async function handleInvoke() {
  try {
    greetResult.value = await invoke<string>('greet', { name: name.value })
  } catch (error) {
    greetResult.value = `调用失败：${String(error)}`
  }
}
</script>

<style scoped>
.shell {
  max-width: 1040px;
  margin: 0 auto;
  padding: 32px 24px 48px;
}

.hero {
  margin-bottom: 24px;
}

.eyebrow {
  margin: 0 0 8px;
  color: var(--color-accent);
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

h1 {
  margin: 0;
  font-size: clamp(28px, 4vw, 42px);
  line-height: 1.05;
}

.summary {
  max-width: 680px;
  margin: 12px 0 0;
  color: var(--color-text-muted);
  line-height: 1.6;
}

.panel-grid {
  display: grid;
  gap: 16px;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

.panel {
  border-radius: 18px;
}

.field-stack {
  display: grid;
  gap: 12px;
}

.field-label {
  font-size: 13px;
  font-weight: 600;
  color: var(--color-text-muted);
}

.date-field,
.text-input,
.primary-button {
  width: 100%;
}

.text-input {
  min-height: 40px;
  padding: 0 12px;
  border: 1px solid var(--color-border);
  border-radius: 12px;
  background: var(--color-surface);
  color: var(--color-text);
}

.primary-button {
  min-height: 40px;
  border: 0;
  border-radius: 12px;
  background: var(--color-accent);
  color: #fff;
  font-weight: 600;
  cursor: pointer;
}

.result {
  margin: 0;
  color: var(--color-text-muted);
  line-height: 1.6;
  word-break: break-word;
}
</style>
