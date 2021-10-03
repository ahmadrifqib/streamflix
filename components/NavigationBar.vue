<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <div class="container mx-auto">
        <b-navbar-brand href="#">StreamFlix</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item href="/">Home</b-nav-item>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <div class="h4 text-white">Rp. 100.000</div>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {}
</script>

<style></style>
