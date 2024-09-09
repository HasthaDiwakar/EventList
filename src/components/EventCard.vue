<template>
  <div
    class="event-card border border-gray-200 rounded-lg p-4 flex flex-col items-center"
  >
    <div class="w-full h-32 bg-gray-300 rounded-lg mb-4">
      <img
        :src="`/${event.image}`"
        alt="Event Image"
        class="w-full h-full object-cover"
      />
    </div>
    <div class="text-center">
      <h3 class="text-lg font-semibold">{{ event.title }}</h3>
      <p class="text-sm text-gray-500">{{ eventDate(event) }}</p>
    </div>
    <button
      class="bg-green-400 text-white py-2 px-4 mt-4 rounded-lg"
      @click="navigateToDetailPage(event.id)"
    >
      View
    </button>
  </div>
</template>

<script>
export default {
  name: "EventCard",
  props: {
    event: {
      type: Object,
      required: true,
    },
  },
  methods: {
    //TODO
    navigateToDetailPage(eventID) {
      console.log(eventID);
    },
  },
  computed: {
    //to split the date and contact to display
    eventDate() {
      return (item) =>
        `${item.start.split("T")[0]} - ${item.end.split("T")[0]}`;
    },
  },
};
</script>
