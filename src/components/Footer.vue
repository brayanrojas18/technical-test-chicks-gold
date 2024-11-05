<script setup lang="ts">
import { ref } from "vue";

const toggleMenu = (event: MouseEvent) => {
  const target = event.currentTarget as HTMLElement;
  target.classList.toggle("active");
};
</script>

<template>
  <div class="footer">
    <div class="footer-header">
      <div class="footer-header-payments">
        <img src="/images/visa.png" />
        <img src="/images/mastercard.png" />
        <img src="/images/american.png" />
        <img src="/images/skrill.png" />
      </div>
      <div class="footer-header-cripto">
        <img src="/images/btcc.png" />
        <img src="/images/eth.png" />
        <img src="/images/btc.png" />
        <img src="/images/lit.png" />
      </div>
      <div class="footer-header-label">and 50+ more</div>
    </div>
    <div class="footer-container">
      <div class="footer-container-social">
        <img src="/images/facebook.png" />
        <img src="/images/instagram.png" />
        <img src="/images/twitter.png" />
        <img src="/images/discord.png" />
      </div>
      <div class="footer-container-separator"></div>
      <div class="footer-container-menu">
        <div class="footer-container-menu-logo">
          <div class="logo">CHICKS GOLD</div>
          <div class="support">support@chicksgold.com</div>
        </div>
        <div class="footer-container-menu-sub" @click="toggleMenu">
          <div class="dropdown">
            <div class="title">Chicks Gold</div>
            <i class="fas fa-chevron-down"></i>
          </div>
          <ul>
            <li>Games</li>
            <li>About Us</li>
            <li>Blog</li>
            <li>Sitemap</li>
          </ul>
        </div>
        <div class="footer-container-menu-sub" @click="toggleMenu">
          <div class="dropdown">
            <div class="title">Support</div>
            <i class="fas fa-chevron-down"></i>
          </div>
          <ul>
            <li>Contact Us</li>
            <li>FAQ</li>
          </ul>
        </div>
        <div class="footer-container-menu-sub" @click="toggleMenu">
          <div class="dropdown">
            <div class="title">Legal</div>
            <i class="fas fa-chevron-down"></i>
          </div>
          <ul>
            <li>Privacy Policy</li>
            <li>Terms of Services</li>
            <li>Copyright Policy</li>
          </ul>
        </div>
        <div class="footer-container-menu-reviews">
          <div>Trustpilot Reviews</div>
          <div style="display: flex; justify-content: center; margin-top: 10px">
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
          </div>
        </div>
      </div>
      <div class="footer-container-copy">
        Copyright © 2017, ChicksGold.com. All Rights Reserved.
      </div>
    </div>
  </div>
</template>
