<script setup lang="ts">
class Item {
  name: string;
  description: string;
  price: number;
  oldPrice: number;
  quantity: number;
  image: string;
  logo: string;
};

defineProps<{
  game: Item
}>()
</script>

<template>
  <div class="card">
    <div class="card-header">
      <div class="card-header-first">
        <div style="display: flex; align-items: center; gap: 5px;">
          <div 
            style="
              width: 5px; 
              height: 5px; 
              background-color: #37e19c; 
              border-radius: 50%; 
              display: inline-block;
            "
          ></div>
          <div>
            ON SALE
          </div>
        </div>
        <div>
          <button>
            In stock
          </button>
        </div>
      </div>
      <div class="card-header-second">
        <input v-model="game.quantity" type="number" min="1">
      </div>
    </div>
    <div class="card-img">
      <img :src="game.image">
    </div>
    <div class="card-title">
      <div>
        {{ game.name }}
      </div>
      <img :src="game.logo" style="width: 25px;">
    </div>
    <div class="card-subtitle">
      ${{ game.price }} <span>${{ game.oldPrice }}</span>
    </div>
    <div class="card-main">
      {{ game.description }}
    </div>
    <div class="card-action">
      <button class="card-action-1">
        DETAILS
      </button>
      <button class="card-action-2">
        ADD <i class="fas fa-shopping-cart" style="padding: 7px; background-color: #444da8; border-radius: 4px;"></i>
      </button>
    </div>
  </div>
</template>

