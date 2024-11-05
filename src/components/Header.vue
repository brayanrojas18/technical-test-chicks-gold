<script setup lang="ts">
import { ref } from "vue";

// DATA
const hovered = ref<string | null>(null);
const buttons = ref([
  { name: "CURRENCY" },
  { name: "ITEMS" },
  { name: "ACCOUNTS" },
  { name: "SERVICES" },
  { name: "SWAP" },
  { name: "SELL" },
]);
const menuVisible = ref(false);

// FUNCTIONS
const setHovered = (name: string | null) => {
  hovered.value = name;
};
const toggleMenu = () => {
  menuVisible.value = !menuVisible.value;
};
</script>

<template>
  <div class="header">
    <div class="content-1">
      <div class="menu-toggle" @click="toggleMenu">☰</div>
      <div class="logo">CHICKS GOLD</div>
      <div class="separator"></div>
      <div :class="['menu', { open: menuVisible }]">
        <button v-if="menuVisible" class="close-menu" @click="toggleMenu">
          ✕
        </button>
        <button
          v-for="button in buttons"
          :key="button.name"
          @mouseover="setHovered(button.name)"
          @mouseout="setHovered(null)"
          class="button-style"
        >
          {{ button.name }}
          <i
            :class="
              hovered === button.name
                ? 'fas fa-chevron-up'
                : 'fas fa-chevron-down'
            "
          ></i>
        </button>
      </div>
    </div>
    <div class="content-2">
      <div class="cart">
        <button @mouseover="setHovered('usd')" @mouseout="setHovered(null)">
          USD
          <i
            :class="
              hovered === 'usd' ? 'fas fa-chevron-up' : 'fas fa-chevron-down'
            "
          ></i>
        </button>
      </div>
      <div class="cart">
        <button><i class="fas fa-shopping-cart"></i>CART (5)</button>
      </div>
      <div class="singin">
        <button class="button">
          SIGN IN <i class="fas fa-user" style="margin-left: 5px"></i>
        </button>
      </div>
    </div>
  </div>
</template>
