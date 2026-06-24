<template>
  <header class="app-header">
    <div class="header-container">
      <h1 class="brand-name">Homes & Beyond</h1>
      <div class="stats-badge">
        Total Properties: <strong>{{ totalCount }}</strong>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    totalCount: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.app-header {
  background-color: #ffffff;
  border-bottom: 1px solid #e2e8f0;
  padding: 1.25rem 2rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}
.header-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.brand-name {
  color: #1a202c;
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0;
}
.stats-badge {
  background-color: #edf2f7;
  color: #4a5568;
  padding: 0.5rem 1rem;
  border-radius: 9999px;
  font-size: 0.9rem;
}
</style>
