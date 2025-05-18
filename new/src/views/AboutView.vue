<template>
  <div class="about responsive-container">
    <h1>About Our Application</h1>
    
    <div class="row">
      <div class="col-12 mb-4">
        <p class="lead">
          This web application is built as part of the COS30043 Interface Design and Development course.
          It demonstrates the use of Vue.js version 3 and Bootstrap to create responsive, interactive web interfaces.
        </p>
      </div>
    </div>
    
    <div class="row mb-4">
      <div class="col-md-6">
        <div class="card">
          <div class="card-header">Your Information</div>
          <div class="card-body">
            <div class="mb-3">
              <label for="firstName" class="form-label">First Name</label>
              <input 
                type="text" 
                class="form-control" 
                id="firstName" 
                v-model="firstName" 
                placeholder="Enter your first name"
              >
            </div>
            <div class="mb-3">
              <label for="lastName" class="form-label">Last Name</label>
              <input 
                type="text" 
                class="form-control" 
                id="lastName" 
                v-model="lastName" 
                placeholder="Enter your last name"
              >
            </div>
          </div>
        </div>
      </div>
      
      <div class="col-md-6">
        <div class="card">
          <div class="card-header">Welcome Message</div>
          <div class="card-body">
            <h5 v-if="firstName && lastName">Hello, {{ firstName }} {{ lastName }}!</h5>
            <p v-if="firstName && lastName">Thank you for visiting our web application.</p>
            <p v-else>Please enter your name to see a personalized welcome message.</p>
          </div>
        </div>
      </div>
    </div>
    
    <div class="row mb-4">
      <div class="col-md-6">
        <div class="card">
          <div class="card-header">Choose a Scene</div>
          <div class="card-body">
            <div class="form-check">
              <input 
                class="form-check-input" 
                type="radio" 
                name="scene" 
                id="mountain" 
                value="mountain" 
                v-model="selectedScene"
              >
              <label class="form-check-label" for="mountain">
                Mountain
              </label>
            </div>
            <div class="form-check">
              <input 
                class="form-check-input" 
                type="radio" 
                name="scene" 
                id="ocean" 
                value="ocean" 
                v-model="selectedScene"
              >
              <label class="form-check-label" for="ocean">
                Ocean
              </label>
            </div>
          </div>
        </div>
      </div>
      
      <div class="col-md-6">
        <div class="card">
          <div class="card-header">Selected Scene</div>
          <div class="card-body">
            <div v-if="selectedScene" class="text-center">
              <img 
                :src="sceneImage" 
                class="img-fluid rounded" 
                :alt="selectedScene + ' scene'"
              >
            </div>
            <p v-else>Please select a scene to view the image.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MountainImage from '../assets/images/mountain.jpg'
import OceanImage from '../assets/images/ocean.jpg'

export default {
  name: 'AboutView',
  data() {
    return {
      firstName: '',
      lastName: '',
      selectedScene: '',
      mountainImage: MountainImage,
      oceanImage: OceanImage
    }
  },
  computed: {
    sceneImage() {
      if (this.selectedScene === 'mountain') {
        return this.mountainImage
      } else if (this.selectedScene === 'ocean') {
        return this.oceanImage
      }
      return ''
    }
  }
}
</script>

<style scoped>
.card {
  height: 100%;
}

img {
  max-height: 200px;
  object-fit: cover;
}
</style>