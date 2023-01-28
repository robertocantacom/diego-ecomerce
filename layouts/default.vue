<template>
  <div>
      <SideBar/>
      <Navbar/>
      <nuxt/>
      <FooterComp/>
    
  
  </div>
</template>

<script>
import Navbar from '../components/Navbar'
import FooterComp from '../components/FooterComponent.vue'
import SideBar from '../components/Sidebar.vue'

export default {
  components: {
    Navbar,
    FooterComp,
    SideBar
  },
  layout: 'default', 
}
</script> 

<style>

</style>