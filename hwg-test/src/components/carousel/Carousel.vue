<template>
    <div class="carousel">
        <div class="carousel-container">
            <div class="carousel-item">
                <img :src="items[currentSlide].image_url" :alt="items[currentSlide].title" class="carousel-image" />
                <div class="carousel-info">
                    <h3>{{ items[currentSlide].title }}</h3>
                </div>
            </div>
        </div>
        <button @click="nextSlide" class="nav-button next">Next</button>
        <button @click="prevSlide" class="nav-button prev">Prev</button>

    </div>
</template>
  
<script>
import { ref, computed } from 'vue';

export default {
    props: {
        data: {
            type: Array,
            required: true,
        },
    },
    setup(props) {
        const items = computed(() => props.data);
        const currentSlide = ref(0);

        const nextSlide = () => {
            currentSlide.value = currentSlide.value + 1;
        };

        const prevSlide = () => {
            currentSlide.value = currentSlide.value - 1;
        };

        return {
            items,
            currentSlide,
            nextSlide,
            prevSlide,
        };
    },
};
</script>
  
<style scoped>
.carousel {
    position: relative;
    max-width: 800px;
    margin: 0 auto;
    overflow: hidden;
}

.nav-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background-color: #333;
    color: #fff;
    padding: 8px;
    border: none;
    cursor: pointer;
}

.prev {
    left: 0;
}

.next {
    right: 0;
}

.carousel-container {
    display: flex;
    transition: transform 0.3s ease;
    overflow: hidden;
}

.carousel-item {
    flex: 0 0 100%;
    box-sizing: border-box;
    margin-right: 16px;
    opacity: 0.5;
    transition: opacity 0.3s ease;
}

.carousel-item img {
    width: 100%;
    border-radius: 8px;
}

.carousel-item.active {
    opacity: 1;
}

.carousel-info {
    margin-top: 8px;
}

.featured-badge {
    background-color: #ffcc00;
    color: #333;
    padding: 4px 8px;
    border-radius: 4px;
    font-weight: bold;
}
</style>
  