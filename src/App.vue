<template>
  <TicketPassHeader />
  <EventDashboard msg="Welcome" />
  <TicketPassFooter />
</template>

<script>
import EventDashboard from './components/EventDashboard.vue'
import TicketPassHeader from './Header/TicketPassHeader.vue'
import TicketPassFooter from './Footer/TicketPassFooter.vue'
export default {
  name: 'App',
  components: {
    TicketPassHeader,
    EventDashboard,
    TicketPassFooter
  },
}
</script> 

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
