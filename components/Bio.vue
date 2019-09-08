<template>
  <div class="bio">
    <img v-if="this.$nuxt.$route.name !== 'index'"
      src="~/static/icon.png"
    />
    <div>
      <p>
        Blog article edited by
        <strong>Stephen Bau</strong> from Design Influences.
      </p>
      <p>Exploring how imagine, design, and build the future together.</p>
    </div>
  </div>
</template>
