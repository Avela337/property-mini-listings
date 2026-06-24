<template>
  <div class="property-card" :class="{ 'unavailable-opacity': !property.available }">
    <div class="image-container">
      <img :src="property.image" :alt="property.title" class="property-image" />
      
      <span v-if="!property.available" class="badge unavailable-badge">Not Available</span>
      <span v-else class="badge available-badge">Available</span>
    </div>

    <div class="card-content">
      <div class="card-header">
        <span class="property-type">{{ property.type }}</span>
        
        <button 
          @click="$emit('toggle-bookmark', property.id)" 
          class="bookmark-btn"
          :class="{ 'is-bookmarked': isBookmarked }"
          :title="isBookmarked ? 'Remove Bookmark' : 'Add Bookmark'"
        >
          
        </button>
      </div>

      <h3 class="property-title">{{ property.title }}</h3>
      <p class="property-location"> {{ property.location }}</p>
      
      <div class="card-footer">
        <span class="property-price">R {{ property.price.toLocaleString() }} <small>/ night</small></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    property: {
      type: Object,
      required: true
    },
    isBookmarked: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.property-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
  position: relative;
  display: flex;
  flex-direction: column;
}
.property-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}
.unavailable-opacity {
  border: 1px solid #fed7d7;
}
.image-container {
  position: relative;
  height: 200px;
  width: 100%;
  background-color: #e2e8f0;
}
.property-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.badge {
  position: absolute;
  top: 12px;
  left: 12px;
  padding: 0.25rem 0.75rem;
  font-size: 0.75rem;
  font-weight: 700;
  border-radius: 6px;
  text-transform: uppercase;
}
.unavailable-badge {
  background-color: #e53e3e;
  color: white;
}
.available-badge {
  background-color: #38a169;
  color: white;
}
.card-content {
  padding: 1.25rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}
.property-type {
  font-size: 0.75rem;
  text-transform: uppercase;
  font-weight: 600;
  color: #718096;
}
.bookmark-btn {
  background: none;
  border: none;
  font-size: 1.4rem;
  color: #cbd5e0;
  cursor: pointer;
  transition: color 0.1s ease;
  line-height: 1;
}
.bookmark-btn:hover {
  color: #a0aec0;
}
.bookmark-btn.is-bookmarked {
  color: #ecc94b;
}
.property-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: #2d3748;
  margin: 0 0 0.5rem 0;
  line-height: 1.4;
}
.property-location {
  font-size: 0.87rem;
  color: #4a5568;
  margin: 0 0 1.25rem 0;
}
.card-footer {
  margin-top: auto;
  border-top: 1px solid #edf2f7;
  padding-top: 0.75rem;
}
.property-price {
  font-size: 1.2rem;
  font-weight: 700;
  color: #2b6cb0;
}
.property-price small {
  font-size: 0.8rem;
  color: #718096;
  font-weight: 400;
}
</style>
