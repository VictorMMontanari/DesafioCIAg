<template>
    <div class="star-rating">
      <span
        v-for="i in maxRating"
        :key="i"
        :class="{ 'star': true, 'filled': i <= currentRating, 'half-filled': i - 0.5 === currentRating }"
        @click="setRating(i)"
      >
        &#9733;
      </span>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps(["avalicao"]);
  
  import { computed } from 'vue';
  
  const maxRating = computed(() => 5); // Set the maximum rating as needed
  const currentRating = computed(() => {
    const roundedRating = Math.round(props.avalicao); // Round the rating to the nearest whole number
    const hasHalfStar = props.avalicao - roundedRating === 0.5; // Check if there's a half star
    return hasHalfStar ? roundedRating - 0.5 : roundedRating;
  });
  
  const setRating = (rating) => {
    // Implement your logic to set the rating, if needed
  };
  </script>
  
  <style scoped>
  .star-rating {
    display: flex;
  }
  
  .star {
    font-size: 24px;
    cursor: pointer;
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
  