<template>
    <div class="autocomplete">
        <input v-model="searchTerm" @input="handleInput" @focus="showSuggestions" @blur="hideSuggestions"
            placeholder="Type to search..." class="search-input" />
        <div v-if="showSuggestion" class="suggestion-container">
            <div v-for="(item, index) in filteredSuggestions" :key="index" @click="selectSuggestion(item)"
                class="suggestion-item">
                {{ item }}
            </div>
        </div>
    </div>
</template>
  
<script>
import { ref, reactive, computed, onMounted, nextTick } from 'vue';

export default {
    props: {
        data: {
            type: Array,
            required: true,
        },
    },
    setup(props) {
        const searchTerm = ref('');
        const showSuggestion = ref(false);

        const suggestions = reactive(props.data.map(val => val.title));

        const filteredSuggestions = computed(() => {
            return suggestions.filter(suggestion => suggestion.toLowerCase().includes(searchTerm.value.toLowerCase()));
        });

        const handleInput = () => {
            showSuggestion.value = true;
        };

        const showSuggestions = () => {
            showSuggestion.value = true;
        };

        const hideSuggestions = () => {
            nextTick(() => {
                showSuggestion.value = false;
            });
        };

        const selectSuggestion = (item) => {
            searchTerm.value = item;
            showSuggestion.value = false;
        };

        // Additional setup if needed, such as fetching data, etc.
        onMounted(() => {
            // Do something on component mount
        });

        return {
            searchTerm,
            showSuggestion,
            suggestions,
            filteredSuggestions,
            handleInput,
            showSuggestions,
            hideSuggestions,
            selectSuggestion,
        };
    },
};
</script>
  
<style scoped>
.autocomplete {
    position: relative;
    display: inline-block;
}

.search-input {
    padding: 8px;
    width: 200px;
    border: 1px solid #ccc;
    border-radius: 4px;
    outline: none;
}

.suggestion-container {
    position: absolute;
    top: 100%;
    left: 0;
    z-index: 2;
    width: 100%;
    max-height: 200px;
    overflow-y: auto;
    border: 1px solid #ccc;
    border-top: none;
    border-radius: 0 0 4px 4px;
    background-color: #fff;
}

.suggestion-item {
    padding: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.suggestion-item:hover {
    background-color: #f0f0f0;
}
</style>
  