<script setup lang="ts">
const props = defineProps<{
  message: string
  customCode: number
  code: string
  statusCode: number
  hint: string | null
  details: string
  isCustomError: boolean
}>()
const error = ref({
  code: 500,
  msg: 'Ops, something went wrong!'
})
if(props.isCustomError) {
  error.value.code = props.customCode
  error.value.msg = props.message
}

if (props.statusCode === 406) {
  error.value.code = 404
  error.value.msg = "Sorry, we couldn't find this page"
}

</script>

<template>
  <div class="error-container">
    <div class="error-content">
      <iconify-icon icon="lucide:triangle-alert" class="error-icon" />

      <h1 v-if="customCode || code" class="error-code">
        {{ customCode || code }}
      </h1>

      <p v-if="statusCode" class="status-code">
        Status Code: {{ statusCode }}
      </p>

      <p class="error-message">{{ message }}</p>

      <div v-if="hint || details" class="error-details">
        <p v-if="hint" class="error-hint">{{ hint }}</p>
        <p v-if="details" class="error-details-text">{{ details }}</p>
      </div>

      <div class="error-footer">
        <p class="error-footer-text">You'll find lots to explore on the home page.</p>
        <RouterLink to="/">
          <Button class="home-button max-w-36">
            Back to homepage
          </Button>
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<!-- <style scoped>
.error-container {
  @apply max-w-2xl mx-auto p-6 text-center;
}

.error-content {
  @apply space-y-4;
}

.error-icon {
  @apply w-12 h-12 mx-auto text-yellow-500;
}

.error-code {
  @apply text-4xl font-bold text-gray-900 dark:text-white;
}

.status-code {
  @apply text-sm text-gray-500 dark:text-gray-400;
}

.error-message {
  @apply text-lg text-gray-700 dark:text-gray-300;
}

.error-details {
  @apply mt-4 space-y-2 text-left;
}

.error-hint {
  @apply text-sm text-yellow-600 dark:text-yellow-400;
}

.error-details-text {
  @apply text-sm text-gray-600 dark:text-gray-400;
}

.error-footer {
  @apply mt-8 pt-6 border-t border-gray-200 dark:border-gray-700;
}

.error-footer-text {
  @apply mb-4 text-gray-500 dark:text-gray-400;
}

.home-button {
  @apply w-full;
}
</style> -->
