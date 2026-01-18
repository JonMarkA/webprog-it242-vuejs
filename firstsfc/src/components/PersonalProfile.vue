<template>
  <div id="bg"></div>
  
  <div id="wrapper">
    <header id="header" v-if="activeTab === 'home'">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
      <div class="logo-container">
        <div class="logo-circle">
          <i class="fa-regular fa-gem"></i>
        </div>
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

      <ul class="icons">
        <li><a href="https://linkedin.com/in/dyonasito"><i class="fa-brands fa-linkedin"></i></a></li>
        <li><a href="https://facebook.com/dyonasito"><i class="fa-brands fa-facebook"></i></a></li>
        <li><a href="https://instagram.com/dyonasito/"><i class="fa-brands fa-instagram"></i></a></li>
        <li><a href="https://github.com/Johanoss"><i class="fa-brands fa-github"></i></a></li>
        <li class="separator"></li>
        <li><a href="resources.html"><i class="fa-regular fa-file-lines"></i></a></li>
      </ul>

      <hr style="margin: 2rem 0; border: 0; border-top: 1px solid rgba(255, 255, 255, 0.2);">

      <div id="contact-app">
        <transition name="fade">
          <form v-if="!submitted" @submit.prevent="submitForm">
            <h3 style="font-size: 0.8rem; letter-spacing: 0.2rem; margin-bottom: 1.5rem; text-transform: uppercase;">Get in Touch</h3>
            
            <div class="field">
              <input type="text" v-model="formData.name" placeholder="Name" required class="contact-field">
            </div>

            <div class="field">
              <input type="email" v-model="formData.email" placeholder="Email" required class="contact-field">
            </div>

            <div class="field">
              <textarea v-model="formData.message" placeholder="Message" rows="3" required class="contact-field" style="resize: none;"></textarea>
            </div>

            <button type="submit" :disabled="loading" class="contact-btn">
              {{ loading ? 'Sending...' : 'Send' }}
            </button>
          </form>
          <div v-else class="success-message" style="padding: 1.5rem; border: 1px solid rgba(255,255,255,0.2); background: rgba(255,255,255,0.05);">
            <p>✨ Thank you, {{ formData.name }}! I'll get back to you soon.</p>
          </div>
        </transition>
      </div>
    </header>

    <div id="main" v-if="activeTab !== 'home'" style="display: flex;">
      <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
      <article v-if="activeTab === 'intro'" style="display: block;">
        <h2 class="major">
          About Me 
          <span class="close" @click="navigateTo('home')"><i class="fa-solid fa-xmark"></i></span>
        </h2>
        <div class="intro-grid">
          <div class="intro-image">
            <img src="./pictures/IMG_2504.JPG" alt="Profile">
          </div>
          <div class="intro-content">
            <p>
                <strong>Name: </strong>Jonathan Mark Agbulos<br><br>
                <strong>Hard Skills: </strong>Basic SQL, Canva, UI<br><br>
                <strong>Interests: </strong>Digital Illustration, Layout Design, Mobile UI Customization, Photography, Games, Data Encoding<br><br>
                <strong>Education: </strong>
            </p>
            <ul>
                <li>
                    SHS: Arellano University Jose Abad Santos Campus
                    <ul>
                        <li>Strand: TECH-VOC - Information &amp; Communications Technology (ICT)</li>
                    </ul>
                </li>
                <li>
                    <span style="display: inline-block; margin-right: 5px;">College: Asia Pacific College</span>
                        <em style="font-size: 0.8rem;">(Current)</em>
                            <ul>
                                <li>Course: Bachelor of Science in Information Technology (BSIT)</li>
                            </ul>
                </li>
            </ul>
            <p><br><strong>Goals in Life: </strong> Wealthy Life</p>
          </div>
        </div>
      </article>

      <article v-if="activeTab === 'projects'" style="display: block;">
        <h2 class="major">
          My Projects
          <span class="close" @click="navigateTo('home')"><i class="fa-solid fa-xmark"></i></span>
        </h2>
        <table>
          <thead>
            <tr>
              <th>Project Name</th>
              <th>Link</th>
            </tr>
          </thead>
          <tbody>
           <tr>
            <td>
              My Simple &amp; Interactive School ID<br>
             <em style="font-size: 0.8rem; opacity: 0.7;">1st Project (Created: October 3, 2025)<br><br>
             NOTE: Best to view this in desktop</em>
            </td>
            <td><a href="https://johanoss.github.io/Projects/school-id/index.html" target="_blank" rel="noopener">View Project</a></td>
           </tr>
            <tr>
             <td>
              My Profile Website<br>
               <em style="font-size: 0.8rem; opacity: 0.7;">2nd Project (Created: January 9, 2026)</em>
             </td>
             <td>
              You're here!
              </td>
            </tr>
         </tbody>
        </table>
      </article>

      <article v-if="activeTab === 'gallery'" style="display: block;">
        <h2 class="major">
          Gallery 
          <span class="close" @click="navigateTo('home')"><i class="fa-solid fa-xmark"></i></span>
        </h2>
        <div class="gallery">
            <div><img src="./pictures/WIN_20241021_08_43_32_Pro.jpg" alt="Gallery 1"></div>
            <div><img src="./pictures/IMG_2506.JPG" alt="Gallery 2"></div>
            <div><img src="./pictures/IMG_2514.JPG" alt="Gallery 3"></div>
            <div><img src="./pictures/IMG_20251123_145257(1).jpg" alt="Gallery 4"></div>
        </div>
      </article>

    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const activeTab = ref('home')
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
/* Path updated to match your folder structure image */
@import "./css/style.css"; 

.fade-enter-active, .fade-leave-active { transition: opacity 0.5s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

/* Styles from your original index.html style tag */
.contact-field { 
  width: 100%; 
  background: rgba(255,255,255,0.05); 
  border: 1px solid rgba(255,255,255,0.2); 
  padding: 0.75rem; 
  color: #fff; 
  margin-bottom: 1rem; 
}
.contact-btn { 
  background: transparent; 
  border: 1px solid #fff; 
  color: #fff; 
  padding: 0.5rem 2rem; 
  cursor: pointer; 
  text-transform: uppercase; 
  font-size: 0.7rem; 
  letter-spacing: 0.2rem; 
  transition: 0.3s; 
}
</style>