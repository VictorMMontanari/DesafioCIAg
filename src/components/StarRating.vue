<script setup>
import { defineProps } from 'vue';

const props = defineProps(["avalicao"]);

import { computed } from 'vue';

const maxRating = computed(() => 5); 
const currentRating = computed(() => {
  const roundedRating = Math.round(props.avalicao); 
  const hasHalfStar = props.avalicao - roundedRating === 0.5; 
  return hasHalfStar ? roundedRating - 0.5 : roundedRating;
});

</script>

<template>
  <div class="star-rating">
    <span v-for="i in maxRating" :key="i"
      :class="{ 'star': true, 'filled': i <= currentRating, 'half-filled': i - 0.5 === currentRating }">
      &#9733;
    </span>
  </div>
</template>
  
<style scoped>
.star-rating {
  display: flex;
}

.star {
  font-size: 24px;
  margin: 0 2px;
}

.filled {
  color: gold;
}

.half-filled::before {
  content: "★";
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  color: gold;
}
</style>
  