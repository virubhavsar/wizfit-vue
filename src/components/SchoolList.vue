<template>
  <!-- Header Section -->
  <header class="header">
    <img :src="bannerImage" alt="WizFit Challenge Logo" class="logo" />
  </header>

  <div class="container">
    <!-- What is WizFit Challenge Section -->
    <section class="challenge-info">
      <h2 class="challenge-title">What is WizFit Challenge?</h2>
      <button class="watch-video-btn">Watch Video</button>
    </section>

    <!-- Main Section -->
    <main class="main-content">
      <img :src="playerImage" alt="Basketball Player" class="main-image" />
      <div class="content-box">
        <h3 class="challenge-question">Are you ready to take the challenge?</h3>
        <p class="download-text">Download Harlem Wizards App</p>
        <div class="app-buttons">
          <img :src="googlePlayImage" alt="Google Play" />
          <img :src="appleStoreImage" alt="App Store" />
        </div>
        <h3 class="text-with-lines">Or you can sign up right now</h3>

        <!-- Campaign Sign Up -->
        <div class="campaign-signup">
          <input
            v-model="searchQuery"
            @input="filterSchools"
            type="text"
            placeholder="Search Campaign Here"
            class="search-campaign"
          />
          <div v-if="loading" class="loading">Loading ...</div>
          <div v-if="error" class="error">{{ error }}</div>
          <div v-if="filteredSchools.length === 0 && !loading" class="no-results">
            No schools found.
          </div>

          <ul class="campaign-list" v-if="filteredSchools.length > 0 && !loading">
            <li v-for="school in filteredSchools" :key="school.id" class="campaign-item">
              <img
                :src="school.logo_url ? school.logo_url : defaultLogo"
                alt="School Logo"
                class="school-logo"
              />
              <div class="school-info">
                <h3 class="school-name">{{ school.school_name }}</h3>
                <p class="school-location">{{ school.city_name }}, {{ school.state_name }}</p>
              </div>
              <button class="join-campaign">Join Campaign</button>
            </li>
          </ul>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import bannerImage from '@/assets/img/banner.png'
import playerImage from '@/assets/img/player.png'
import googlePlayImage from '@/assets/img/google-store.png'
import appleStoreImage from '@/assets/img/apple-store.png'
import defaultLogo from '@/assets/img/no_img.png'
import '@/assets/css/WizFitChallenge.css'
import { API_ENDPOINTS } from '@/config/config'

export default {
  name: 'WizFitChallenge',
  data() {
    return {
      bannerImage,
      playerImage,
      googlePlayImage,
      appleStoreImage,
      defaultLogo,
      searchQuery: '',
      schools: [],
      filteredSchools: [],
      loading: false,
      error: null
    }
  },
  methods: {
    async fetchSchools() {
      this.loading = true
      this.error = null

      try {
        const response = await axios.get(API_ENDPOINTS.SCHOOLS)
        this.schools = response.data.school_list
        this.filterSchools()
      } catch (err) {
        this.error = 'Failed to load schools. Please try again.'
      } finally {
        this.loading = false
      }
    },
    filterSchools() {
      if (this.searchQuery) {
        const query = this.searchQuery.toLowerCase()
        this.filteredSchools = this.schools.filter(
          (school) =>
            school.school_name.toLowerCase().includes(query) ||
            school.city_name.toLowerCase().includes(query) ||
            school.state_name.toLowerCase().includes(query)
        )
      } else {
        this.filteredSchools = this.schools
      }
    }
  },
  mounted() {
    this.fetchSchools()
  },
  watch: {
    searchQuery: 'filterSchools'
  }
}
</script>
