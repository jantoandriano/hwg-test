<template>
    <div class="photo-gallery">
        <div v-for="(item, index) in featuredItems" :key="index" class="gallery-item" @mouseover="showTooltip(index)"
            @mouseleave="hideTooltip">
            <img :src="item.image_url" :alt="item.title" class="gallery-image" />
            <div class="gallery-info">
                <h3>{{ item.title }}</h3>
                <p>Rating: {{ item.rating }}</p>
                <span v-if="item.is_featured" class="featured-badge">Featured</span>
            </div>
            <div v-if="tooltipIndex === index" class="tooltip">
                This is {{ item.title }}
            </div>
        </div>
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
        const featuredItems = computed(() => props.data.filter(item => item.is_featured));
        const tooltipIndex = ref(null);

        const showTooltip = (index) => {
            tooltipIndex.value = index;
        };

        const hideTooltip = () => {
            tooltipIndex.value = null;
        };

        return {
            featuredItems,
            tooltipIndex,
            showTooltip,
            hideTooltip,
        };
    },
};
</script>
  
<style scoped>

.photo-gallery {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
}

.gallery-item {
    position: relative;
    margin: 16px;
    text-align: center;
    cursor: pointer;
}

.gallery-image {
    width: 100%;
    max-width: 300px;
    border-radius: 8px;
}

.gallery-info {
    margin-top: 8px;
}

.featured-badge {
    background-color: #ffcc00;
    color: #333;
    padding: 4px 8px;
    border-radius: 4px;
    font-weight: bold;
}

.tooltip {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    background-color: lightgoldenrodyellow;
    color: black;
    padding: 4px 8px;
    border-radius: 4px;
    opacity: 0.8;
    display: none;
    z-index: 1;
    /* Ensure tooltip is in front of the image */
}

.gallery-item:hover .tooltip {
    display: block;
}
</style>
  