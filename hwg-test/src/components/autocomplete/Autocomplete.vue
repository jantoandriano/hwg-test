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
import { ref, computed } from 'vue';

export default {
    data() {
        return {
            searchTerm: '',
            suggestions: ['Apple', 'Banana', 'Cherry', 'Date', 'Fig', 'Grape', 'Kiwi', 'Lemon', 'Mango', 'Orange'],
            showSuggestion: false,
        };
    },
    computed: {
        filteredSuggestions() {
            return this.suggestions.filter(suggestion => suggestion.toLowerCase().includes(this.searchTerm.toLowerCase()));
        },
    },
    methods: {
        handleInput() {
            this.showSuggestion = true;
        },
        showSuggestions() {
            this.showSuggestion = true;
        },
        hideSuggestions() {
            // Use nextTick to delay hiding suggestions, allowing click events to be captured first
            this.$nextTick(() => {
                this.showSuggestion = false;
            });
        },
        selectSuggestion(item) {
            this.searchTerm = item;
            this.showSuggestion = false;
        },
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
  