<template>
  <div class="app">
    <nav class="navbar">
      <h2>Edwin Charles</h2>

      <div class="nav-links">
        <div class="home-dropdown">
          <a
            href="#home"
            @click="showAdminMenu = !showAdminMenu"
          >
            Home
          </a>

          <div v-if="showAdminMenu" class="admin-dropdown">
            <a
              href="https://edwin-portfolio-backend.onrender.com/admin"
              target="_blank"
            >
              Control Room
            </a>
          </div>
        </div>  
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#experience">Experience</a>
        <a href="#projects">Projects</a>
        <a href="#contact">Contact</a>
      </div>

      <div class="theme-menu">
        <button class="theme-toggle" @click="showThemes = !showThemes">
          🎨
        </button>

        <div v-if="showThemes" class="theme-dropdown">
          <div @click="changeTheme('blue')" class="theme-item">
            <span class="theme-color blue"></span>
            Blue Tech
          </div>

          <div @click="changeTheme('purple')" class="theme-item">
            <span class="theme-color purple"></span>
            Purple Modern
          </div>

          <div @click="changeTheme('green')" class="theme-item">
            <span class="theme-color green"></span>
            Green Cyber
          </div>

          <div @click="changeTheme('orange')" class="theme-item">
            <span class="theme-color orange"></span>
            Orange Sunset
          </div>
        </div>
      </div>
    </nav>

    <section id="home" class="hero">
      <div class="hero-left">
        <button @click="toggleShortProfile" class="show-profile-btn">
          <i class="fa-solid fa-id-card"></i>
          My Short Profile
        </button>

        <div v-if="showShortProfile" class="short-profile-card">
          <img
            v-if="profileImage"
            :src="profileImage"
            class="profile-photo"
          />

          <h3>{{ profile.name }}</h3>

          <p><strong>Nationality:</strong> {{ profile.nationality }}</p>
          <p><strong>Marital Status:</strong> {{ profile.marital_status }}</p>
          <p><strong>Profession:</strong> {{ profile.profession }}</p>
          <p><strong>Location:</strong> {{ profile.location }}</p>
        </div>
      </div>

      <div class="hero-text">
       <p class="badge">{{ profile.badge }}</p>

        <h1>
          {{ profile.hero_title }} <span>{{ profile.name }}</span>
        </h1>

        <p>
          {{ profile.hero_description }}
        </p>

        <div class="hero-buttons">
          <a href="#projects" class="btn primary" > <i class="fa-solid fa-folder-open"></i>View Projects</a>
          <a href="#contact" class="btn secondary"><i class="fa-solid fa-paper-plane"></i>Contact Me</a>
          <a v-if="cvFile?.url" :href="cvFile.url" target="_blank" class="btn cv-btn">
            <i class="fa-solid fa-file-arrow-down"></i>
            Download CV
          </a>
        </div>
      </div>

      <div class="hero-card">
        <h3>
          <i class="fa-solid fa-bolt"></i>
          Portfolio Summary
        </h3>

        <p class="typing-text" :style="{ color: currentColor }">
          {{ displayedText }}<span class="cursor">|</span>
        </p>
      </div>
    </section>
    <section id="about" class="section">
      <h2><i class="fa-solid fa-user"></i> About Me</h2>

      <div class="about-card">

        <p>{{ about.paragraph_one }}</p>

        <p>{{ about.paragraph_two }}</p>

        <p>{{ about.paragraph_three }}</p>

      </div>
    </section>
    <section id="skills" class="section">
      <h2><i class="fa-solid fa-lightbulb"></i> Skills</h2>

      <div class="grid">
        <div class="card" v-for="skill in skills" :key="skill.title">
          <h3>{{ skill.title }}</h3>
          <p>{{ skill.description }}</p>
        </div>
      </div>
    </section>

    <section id="experience" class="section">
      <h2><i class="fa-solid fa-briefcase"></i> Experience</h2>

      <div class="timeline">

        <div
          class="timeline-item"
          v-for="experience in experiences"
          :key="experience.id"
        >

          <h3>{{ experience.title }}</h3>

          <h4>{{ experience.company }}</h4>

          <p>{{ experience.description }}</p>

        </div>

      </div>
    </section>

    <section id="projects" class="section">
      <h2><i class="fa-solid fa-code"></i> Projects</h2>

      <div class="grid">
        <div class="card project" v-for="project in projects" :key="project.title">
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>

          <div class="tags">
          <span
            v-for="tag in project.tags"
            :key="tag"
            class="tag-item"
          >
            <i
              v-if="tag === 'Laravel'"
              class="fa-brands fa-laravel"
            ></i>

            <i
              v-else-if="tag === 'Vue.js'"
              class="fa-brands fa-vuejs"
            ></i>

            <i
              v-else-if="tag === 'Python'"
              class="fa-brands fa-python"
            ></i>

            <i
              v-else-if="tag === 'MySQL'"
              class="fa-solid fa-database"
            ></i>

            <i
              v-else-if="tag === 'Networking'"
              class="fa-solid fa-network-wired"
            ></i>

             <i
              v-else-if="tag === 'Javascript'"
              class="fa-brands fa-square-js"
            ></i>
            <i
              v-else-if="tag === 'R'"
              class="fa-solid fa-chart-line"
            ></i>
            <i
              v-else-if="tag === 'PHP'"
              class="fa-brands fa-php"
            ></i>

            <i
              v-else-if="tag === 'HTML'"
              class="fa-brands fa-html5"
            ></i>

            <i
              v-else-if="tag === 'CSS'"
              class="fa-brands fa-css3-alt"
            ></i>

            <i
              v-else-if="tag === 'GitHub'"
              class="fa-brands fa-github"
            ></i>

            {{ tag }}
          </span>
        </div>
        </div>
      </div>
    </section>

    <section id="contact" class="section contact">
      <h2><i class="fa-solid fa-envelope"></i> Contact Me</h2>

      <div class="contact-container">

        <!-- EMAIL -->

        <div class="contact-box email-box">
          <div class="contact-icon">
            <i class="fas fa-envelope"></i>
          </div>

          <h3>Email Address</h3>

          <a href="mailto:edwinbayacharlea@gmail.com">
            edwinbayacharlea@gmail.com
          </a>
        </div>

        <!-- WHATSAPP -->

        <div class="contact-box whatsapp-box">
          <div class="contact-icon">
            <i class="fab fa-whatsapp"></i>
          </div>

          <h3>WhatsApp Numbers</h3>

          <a href="https://wa.me/255678815389" target="_blank">
            0678815389
          </a>

          <a href="https://wa.me/255744815389" target="_blank">
            0744815389
          </a>
        </div>

        <!-- PHONE -->

        <div class="contact-box phone-box">
          <div class="contact-icon">
            <i class="fas fa-phone-alt"></i>
          </div>

          <h3>Phone Numbers</h3>

          <a href="tel:+255744815389">
            0744815389
          </a>

          <a href="tel:+255635045389">
            0635045389
          </a>
        </div>
        <div class="contact-box github-box">
          <div class="contact-icon">
            <i class="fa-brands fa-github"></i>
          </div>

          <h3>GitHub</h3>

          <a :href="profile.github_url" target="_blank" class="github-link" >
            Visit My GitHub
          </a>
        </div>

      </div>

      <div class="message-box">
        <h3>Send Me a Message</h3>

        <form @submit.prevent="submitForm">
          <input v-model="form.name" type="text" placeholder="Your Name" required />
          <input v-model="form.email" type="email" placeholder="Your Email" required />
          <input v-model="form.subject" type="text" placeholder="Subject" required />
          <textarea v-model="form.message" placeholder="Your Message" required></textarea>

          <button type="submit">Send Message</button>
        </form>

        <p v-if="successMessage" class="success">{{ successMessage }}</p>
        <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
      </div>
    </section>

    <footer>
      <p>© {{ new Date().getFullYear() }} Edwin Charles. All rights reserved.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const API_URL = import.meta.env.VITE_API_URL
console.log('API URL:', API_URL)

const showThemes = ref(false)
const profile = ref({})
const profileImage = ref(null)
const showShortProfile = ref(false)
const about = ref({})


const skills = ref([])
const projects = ref([])

const summaries = ref([])
const experiences = ref([])

const fetchSummaries = async () => {
  const response = await fetch(`${API_URL}/portfolio-summaries`)
  summaries.value = await response.json()

  if (summaries.value.length > 0) {
    currentColor.value = summaries.value[0].color
    typeSummary()
  }
}

const displayedText = ref('')
const currentColor = ref('#38bdf8')

let summaryIndex = 0
let letterIndex = 0

const typeSummary = () => {
  if (summaries.value.length === 0) {
    return
  }

  const currentSummary = summaries.value[summaryIndex]
  currentColor.value = currentSummary.color

  if (letterIndex < currentSummary.text.length) {
    displayedText.value += currentSummary.text.charAt(letterIndex)
    letterIndex++

    setTimeout(typeSummary, 90)
  } else {
    setTimeout(() => {
      displayedText.value = ''
      letterIndex = 0
      summaryIndex = (summaryIndex + 1) % summaries.value.length
      typeSummary()
    }, 1800)
  }
}
const fetchProfile = async () => {
  const response = await fetch(`${API_URL}/profile`)
  const data = await response.json()

  profile.value = data
  profileImage.value = data.profile_image
}

const fetchAbout = async () => {
  const response = await fetch(`${API_URL}/portfolio-about`)
  const data = await response.json()

  about.value = data
}
const toggleShortProfile = () => {
  showShortProfile.value = !showShortProfile.value
}
const form = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const successMessage = ref('')
const errorMessage = ref('')

const submitForm = async () => {
  successMessage.value = ''
  errorMessage.value = ''

  try {
    const response = await fetch(`${API_URL}/contact-messages`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json'
      },
      body: JSON.stringify(form.value)
    })

    if (!response.ok) {
      throw new Error('Message failed')
    }

    successMessage.value = 'Your message has been sent successfully.'

    form.value = {
      name: '',
      email: '',
      subject: '',
      message: ''
    }
  } catch (error) {
    errorMessage.value = 'Failed to send message. Please try again.'
  }
}

const changeTheme = (theme) => {
  document.body.classList.remove(
    'theme-blue',
    'theme-purple',
    'theme-green',
    'theme-orange'
  )

  document.body.classList.add(`theme-${theme}`)
  showThemes.value = false
}


const fetchSkills = async () => {
  const response = await fetch(`${API_URL}/skills`)
  const data = await response.json()

  skills.value = data
}

const fetchProjects = async () => {
  const response = await fetch(`${API_URL}/projects`)
  const data = await response.json()

  projects.value = data
}

const fetchExperiences = async () => {
  const response = await fetch(`${API_URL}/experiences`)
  const data = await response.json()

  experiences.value = data
}

const cvFile = ref(null)

const fetchCvFile = async () => {
  const response = await fetch(`${API_URL}/cv-file`)
  cvFile.value = await response.json()
}

onMounted(() => {
  document.body.classList.add('theme-blue')
  fetchProfile()
  fetchSummaries()
  fetchAbout()
  fetchSkills()
  fetchProjects()
  fetchExperiences()
  fetchCvFile()
})

</script>