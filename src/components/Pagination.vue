<script lang="ts" setup>
  import { ref, computed, defineProps, defineEmits } from 'vue';

  const props = defineProps({
    itemsPerPage: {
      type: Number,
      default: 15
    },
    totalItems: {
      type: Number,
      required: true
    }
  });

  const emit = defineEmits(['page-changed']);

  const currentPage = ref(1);
  const totalPages = computed(() => Math.ceil(props.totalItems / props.itemsPerPage));

  const prevPage = () => {
    if (currentPage.value > 1) {
      currentPage.value--;
      emit('page-changed', currentPage.value);
    }
  };

  const nextPage = () => {
    if (currentPage.value < totalPages.value) {
      currentPage.value++;
      emit('page-changed', currentPage.value);
    }
  };

  const changePage = (page) => {
    if (page !== '...') {
      currentPage.value = page;
      emit('page-changed', currentPage.value);
    }
  };

  const visiblePages = computed(() => {
    let pages = [];
    if (totalPages.value <= 5) {
      for (let i = 1; i <= totalPages.value; i++) {
        pages.push(i);
      }
    } else {
      const startPage = Math.max(1, currentPage.value - 2);
      const endPage = Math.min(totalPages.value, currentPage.value + 2);

      for (let i = startPage; i <= endPage; i++) {
        pages.push(i);
      }

      if (startPage > 1) {
        pages.unshift(1, '...');
      }

      if (endPage < totalPages.value) {
        pages.push('...', totalPages.value);
      }
    }
    return pages;
  });
</script>

<template>
  <div class="pagination">
    <button @click="prevPage" :disabled="currentPage === 1">
        <i class="fas fa-chevron-left"></i>
    </button>
    <span
      v-for="page in visiblePages"
      :key="page"
      @click="changePage(page)"
      :class="{ active: currentPage === page }"
    >
      {{ page }}
    </span>
    <button @click="nextPage" :disabled="currentPage === totalPages">
        <i class="fas fa-chevron-right"></i>
    </button>
  </div>
</template>
