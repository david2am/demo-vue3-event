<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'

const event = ref(null)
const props = defineProps({
    id: {
        type: String,
        required: true
    }
})

onMounted(async () => {
    try {
        const { data } = await EventService.getEvent(props.id)
        event.value = data
    } catch (error) {
        console.error(error)
    }
})
</script>

<template>
    <div v-if="event">
        <h1>{{ event.title }}</h1>
        <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
        <p>{{ event.description }}</p>
    </div>
</template>
