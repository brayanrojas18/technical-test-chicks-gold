<script setup lang="ts">
import { ref, reactive, computed } from "vue";
import { data } from "./boot/data";

// COMPONENTS
import Header from "./components/Header.vue";
import Card from "./components/Card.vue";
import Pagination from "./components/Pagination.vue";
import Footer from "./components/Footer.vue";

class Item {
  name?: string;
  description?: string;
  price?: number;
  oldPrice?: number;
  quantity?: number;
  image?: string;
  logo?: string;
}

// DATA
const games = ref<Item[]>(data);
const selects = reactive([
  { id: "select1", icon: "fas fa-gamepad", value: "", isActive: false },
  {
    id: "select2",
    icon: "fas fa-money-bill-wave",
    value: "all",
    isActive: true,
  },
  { id: "select3", icon: "fas fa-feather-alt", value: "all", isActive: true },
  { id: "select4", icon: "fas fa-filter", value: "featured", isActive: true },
]);

const itemsPerPage = ref(15);
const currentPage = ref(1);

const paginatedGames = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value;
  const end = start + itemsPerPage.value;
  return games.value.slice(start, end);
});

// FUNCTIONS
const onSelectChange = (select: any) => {
  select.isActive = select.value !== "";
};

const onPageChanged = (newPage: number) => {
  currentPage.value = newPage;
};
</script>

<template>
  <header>
    <Header />
  </header>

  <main class="main">
    <div class="content">
      <div class="title">Condimentum consectetur</div>
      <div class="filters">
        <div class="field">
          <label :for="selects[0].id"><i :class="selects[0].icon"></i></label>
          <div class="select-wrapper">
            <select
              :id="selects[0].id"
              v-model="selects[0].value"
              @change="onSelectChange(selects[0].value)"
              style="padding-top: 15px"
            >
              <option value="all" disabled selected hidden>All</option>
            </select>
            <label
              :for="selects[0].id"
              class="select-placeholder"
              :class="{ active: selects[0].isActive }"
              >Select a game</label
            >
          </div>
        </div>
        <div class="field">
          <label for="search"><i class="fas fa-search"></i></label>
          <input
            type="search"
            id="search"
            placeholder="Search"
            style="padding-top: 8px; padding: 10px"
          />
        </div>
        <div class="field">
          <label :for="selects[1].id"
            ><i :class="selects[1].icon" style="color: #37e19c"></i
          ></label>
          <div class="select-wrapper">
            <select
              :id="selects[1].id"
              v-model="selects[1].value"
              @change="onSelectChange(selects[1].value)"
              style="padding-top: 12px"
            >
              <option value="all" disabled selected hidden>All</option>
            </select>
            <label
              :for="selects[1].id"
              class="select-placeholder"
              :class="{ active: selects[1].isActive }"
              >Price</label
            >
          </div>
          <label :for="selects[2].id"
            ><i :class="selects[2].icon" style="color: #37e19c"></i
          ></label>
          <div class="select-wrapper">
            <select
              :id="selects[2].id"
              v-model="selects[2].value"
              @change="onSelectChange(selects[2].value)"
              style="padding-top: 12px"
            >
              <option value="all" disabled selected hidden>All</option>
            </select>
            <label
              :for="selects[2].id"
              class="select-placeholder"
              :class="{ active: selects[2].isActive }"
              >Item Type</label
            >
          </div>
        </div>
      </div>
      <div class="gallery-container">
        <div class="gallery-container-header">
          <div
            class="subtitle-gallery"
            style="color: #ffffffaf; font-weight: 600"
          >
            Showing {{ games.length }} - from {{ games.length }}
          </div>
          <div class="field">
            <label :for="selects[3].id"><i :class="selects[3].icon"></i></label>
            <div class="select-wrapper">
              <select
                :id="selects[3].id"
                v-model="selects[3].value"
                @change="onSelectChange(selects[3].value)"
              >
                <option value="featured" disabled selected hidden>
                  Featured
                </option>
              </select>
              <label
                :for="selects[3].id"
                class="select-placeholder"
                :class="{ active: selects[3].isActive }"
                >Sort By</label
              >
            </div>
          </div>
        </div>
        <div class="lists-card">
          <Card
            v-for="(game, index) in paginatedGames"
            :key="index"
            :game="game"
          />
        </div>
        <Pagination
          :totalItems="games.length"
          :itemsPerPage="itemsPerPage"
          @page-changed="onPageChanged"
        />
      </div>
    </div>
  </main>

  <footer>
    <Footer />
  </footer>
</template>
