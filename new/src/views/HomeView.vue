<template>
  <div class="home responsive-container">
    <div class="row">
      <div class="col-12">
        <h1>Welcome to Our Web Application</h1>
        <p class="lead">
          This is a modern web application built with Vue.js and Bootstrap, designed to showcase
          interactive features and best practices in web development.
        </p>
      </div>
    </div>
    
    <div class="row mt-4">
      <div class="col-md-6 mb-4">
        <div class="card">
          <img src="../assets/images/home-image1.jpg" class="card-img-top" alt="Feature Image 1">
          <div class="card-body">
            <h5 class="card-title">Explore Our Features</h5>
            <p class="card-text">Discover the powerful features of our web application and how they can benefit you.</p>
          </div>
        </div>
      </div>
      
      <div class="col-md-6 mb-4">
        <div class="card">
          <img src="../assets/images/home-image2.jpg" class="card-img-top" alt="Feature Image 2">
          <div class="card-body">
            <h5 class="card-title">Stay Updated</h5>
            <p class="card-text">Check out our news section to stay updated with the latest announcements and releases.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView'
}
</script>

<style scoped>
.home img {
  max-height: 250px;
  object-fit: cover;
}

/* Small devices (phones) */
@media (max-width: 576px) {
  .home img {
    max-height: 180px;
  }
}

/* Medium devices (tablets) */
@media (min-width: 577px) and (max-width: 991px) {
  .home img {
    max-height: 220px;
  }
}
</style>