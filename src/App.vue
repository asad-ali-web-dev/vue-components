<template>
  <NavbarV1 
    logo="Adak" 
    :links="[
      {title: 'Home', href: '#'},
      {title: 'Portfolio', href: '#'},
      {title: 'Blog', href: '#'},
      {title: 'About', href: '#'},
      {title: 'Contact', href: '#'}
    ]" 
    size="md"
    bgColor="purple"
    bgIntensity="400"
    textColor="white"
  />
</template>

<script>
import NavbarV1 from "./components/Navbars/Navbar-v1/NavbarV1.vue"

export default {
  name: 'App',
  components: {
    NavbarV1
  }
}
</script>
