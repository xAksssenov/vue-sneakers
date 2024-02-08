<script setup>
import Card from './Card.vue'

defineProps({
    items: Array
})

const onClickAdd = () => {
    alert('Добавить')
}
</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <Card
            v-for="items in items"
            :key="items.id"
            :title="items.title"
            :imageUrl="items.imageUrl"
            :price="items.price"
            :isFavorite="false"
            :isAdded="true"
            :onClickAdd="onClickAdd"
            :onClickFavorite="onClickAdd"
        />
    </div>
</template>
