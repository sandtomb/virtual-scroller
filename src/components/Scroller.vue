<script>
import { ref } from 'vue';
import { RecycleScroller } from 'vue-virtual-scroller';

export default {
    setup() {
        const items = ref([])
        const domElemCount = ref(0)
        const counter = () => {
            domElemCount.value = document.getElementsByTagName('*').length
        }

        return {
            items,
            domElemCount,
            counter
        }
    },
    mounted() {
        const newItems = []
        const numbers = [...Array(1000).keys()]
        for (const number in numbers) {
            const randomString = (Math.random() + 1).toString(36).substring(7)
            newItems.push({ id: number, name: randomString})
        }
        this.items.value = newItems
    },
}
</script>

<template>

    DOM Elements: {{ domElemCount }} <button @click="counter"></button>

    <div class="wrapper">

        <RecycleScroller
            key="true"
            ref="scroller"
            class="scroller"
            :items="this.items.value"
            :item-size="32"
            :page-mode="false"
            key-field="id"
        >

        <template #default="props">
            <div>
                {{ props.item.id }} : {{ props.item.name }}
            </div>
        </template>

        </RecycleScroller>

    </div>

</template>

<style scoped>

.wrapper {
    height: 100vh;
}

.scroller {
    width: 100%;
    height: 100%;
}

</style>
