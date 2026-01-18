<template>
  <div id="bg"></div>
  <div id="wrapper">
    
    <header id="header" v-if="activeTab === 'home'">
      <div class="logo-container">
        <div class="logo-circle"><i class="fa-regular fa-gem"></i></div>
      </div>
      <div class="content">
        <h1>Welcome, Visitor!</h1>
        <p>Hi! I'm Jonathan Mark and this is my profile website!</p>
      </div>
      <nav>
        <ul>
          <li><a href="#" @click.prevent="navigateTo('intro')">Intro</a></li>
          <li><a href="#" @click.prevent="navigateTo('projects')">Projects</a></li>
          <li><a href="#" @click.prevent="navigateTo('gallery')">Gallery</a></li>
        </ul>
      </nav>
      
      <div id="contact-app">
        <form v-if="!submitted" @submit.prevent="submitForm">
          <button type="submit" :disabled="loading" class="contact-btn">
            {{ loading ? 'Sending...' : 'Send' }}
          </button>
        </form>
        <div v-else class="success-message">
           <p>✨ Thank you, {{ formData.name }}!</p>
        </div>
      </div>
    </header>

    <div id="main" v-if="activeTab !== 'home'" style="display: flex;">
      
      <article v-if="activeTab === 'intro'" style="display: block;">
        <h2 class="major">
          About Me 
          <span class="close" @click="navigateTo('home')"><i class="fa-solid fa-xmark"></i></span>
        </h2>
        <div class="intro-grid">
          <div class="intro-image">
            <img src="@/assets/pictures/IMG_2504.JPG" alt="Profile">
          </div>
          <div class="intro-content">
            <p><strong>Name: </strong>Jonathan Mark Agbulos</p>
            </div>
        </div>
      </article>

      </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

// State for Navigation
const activeTab = ref('home') // 'home', 'intro', 'projects', or 'gallery'

// State for Contact Form
const submitted = ref(false)
const loading = ref(false)
const formData = reactive({ name: '', email: '', message: '' })

const navigateTo = (tab) => {
  activeTab.value = tab
}

const submitForm = async () => {
  loading.value = true
  const formspreeUrl = 'https://formspree.io/f/xgoowzzy'
  try {
    const response = await fetch(formspreeUrl, {
      method: 'POST',
      headers: { 'Accept': 'application/json', 'Content-Type': 'application/json' },
      body: JSON.stringify(formData)
    })
    if (response.ok) { submitted.value = true } 
    else { alert('Oops! Problem submitting form.') }
  } catch (error) {
    alert('Connection error.')
  } finally { loading.value = false }
}
</script>

<style>
@import "@./components/css/style.css";

.fade-enter-active, .fade-leave-active { transition: opacity 0.5s ease; }
.contact-field { width: 100%; background: rgba(255,255,255,0.05); /* ... */ }
</style>