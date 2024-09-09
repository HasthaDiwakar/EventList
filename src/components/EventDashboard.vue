<template>
  <div class="container mx-auto p-6">
    <!-- Event Cards Grid before loading the events-->
    <div v-if="loading" class="text-center h-96 min-h-96">Loading...</div>

    <!-- Event Cards Grid if the events are not available-->
    <div v-else-if="events.length === 0" class="text-center h-96 min-h-96">No Events Available</div>

    <!-- Event Cards Grid if the events are available-->
    <div v-else>
      <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-6 mb-6">
        <EventCard
          v-for="event in paginatedEvents"
          :key="event.id"
          :event="event"
        />
      </div>

      <!-- Pagination Controls -->
      <div class="flex justify-center space-x-2 mt-6">
        <button
          v-for="page in totalPages"
          :key="page"
          @click="currentPage = page"
          :class="{
            'bg-green-400 text-white': currentPage === page,
            'bg-gray-200 text-gray-700': currentPage !== page,
          }"
          class="px-4 py-2 rounded-lg"
        >
          {{ page }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import EventCard from "./EventCard.vue";

export default {
  components: {
    EventCard,
  },
  data() {
    return {
      events: [], // All events stored in events-data.json inside data folder is fetched from the server using json-server 
      loading: true, // To display a loading state while fetching
      currentPage: 1, // To keep track of the current page in Pagination
      perPage: 8, // Number of events per page to display in the pagiantion
    };
  },
  computed: {
    totalPages() {
      // Calculate total number of pages
      return Math.ceil(this.events.length / this.perPage);
    },
    paginatedEvents() {
      // Slice the events array to only show events for the current page
      const start = (this.currentPage - 1) * this.perPage;
      const end = start + this.perPage;
      return this.events.slice(start, end);
    },
  },
  mounted() {
    // Fetch the events data from json-server
    fetch("http://localhost:3000/events")
      .then((response) => response.json())
      .then((data) => {
        this.events = data;
        this.loading = false;
      })
      .catch((error) => {
        console.error("Error fetching data:", error);
        this.loading = false;
      });
  },
};
</script>
<style></style>
