<template>
  <div class="card h-100">
    <div class="card-header d-flex justify-content-between align-items-center">
      <span class="badge bg-primary">{{ news.category }}</span>
      <small class="text-muted">{{ formattedDate }}</small>
    </div>
    <div class="card-body">
      <h5 class="card-title">{{ news.title }}</h5>
      <p class="card-text">{{ news.content }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewsItem',
  props: {
    news: {
      type: Object,
      required: true
    }
  },
  computed: {
    formattedDate() {
      const date = new Date(this.news.date)
      return date.toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'short',
        day: 'numeric'
      })
    }
  }
}
</script>

<style scoped>
.card-title {
  font-size: 1.1rem;
}
</style>