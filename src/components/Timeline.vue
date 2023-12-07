<template>
  <div class="timeline">
    <div v-for="(event, index) in sortedEvents" :key="index" class="event" @click="toggleDetails(index)">
      <div class="header">
        <h2>{{ event.title }}</h2>
        <h3>{{ event.date }}</h3>
      </div>
      <p v-if="event.showDetails">{{ event.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    events: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      sortedEvents: [],
    };
  },
  methods: {
    sortEvents() {
      this.sortedEvents = this.events.sort((a, b) => new Date(a.date) - new Date(b.date));
    },
    toggleDetails(index) {
      this.sortedEvents[index].showDetails = !this.sortedEvents[index].showDetails;
    },
  },
  mounted() {
    this.sortEvents();
    this.sortedEvents.forEach((event) => {
      this.$set(event, 'showDetails', false);
    });
  },
};
</script>

<style scoped>
.timeline {
  background-color: #f0f0f0;
  padding: 20px;
  margin: 20px;
  border-radius: 10px;
}

.event {
  background-color: #3498db;
  padding: 20px;
  margin: 20px;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.event:hover {
  transform: scale(1.05);
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.event h2 {
  margin-bottom: 10px;
  color: #ecf0f1;
}

.event h3 {
  margin-bottom: 15px;
  color: #2c3e50;
}

.event p {
  display: none;
  color: #ecf0f1;
}

.event:hover p {
  display: block;
  margin-top: 10px;
}
</style>
