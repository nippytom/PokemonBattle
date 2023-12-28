<script setup>
const props = defineProps({
  name: {
    type: String,
    default: ''
  },
  sprites: {
    type: Object,
    default: () => { }
  },
  stats: {
    type: Array,
    default: () => []
  },
  isWinner: {
    type: Boolean,
    default: false
  }
})

const statsToShow = ['hp', 'attack', 'speed']
</script>

<template>
  <div>
    <div>
      <img
        :src="props.sprites.front_default"
        :alt="props.name"
      >
      <h2>
        {{ props.name }}
      </h2>
      <div
        v-for="stat in props.stats"
        :key="stat.stat.name"
      >
        <template v-if="statsToShow.includes(stat.stat.name)">
          {{ stat.stat.name }}: {{ stat.base_stat }}
        </template>
      </div>
      <div
        style="margin-top: 10%; color: #0000FF;"
        v-if="props.isWinner"
      >
        Winner!
      </div>
    </div>
  </div>
</template>