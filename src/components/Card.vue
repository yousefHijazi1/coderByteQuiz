<template lang="">
    <div>
      <h2>Search</h2>
      <input 
        type="text" 
        v-model="searchQuery" 
        placeholder="search for a keyword"
        @input="filterCards"
      />
  
      <div v-if="filteredCards.length > 0" class="">
        <div v-for="(card, index) in filteredCards" :key="index" class="card mb-3">
            
                <div class="card-body">
                    <h5 class="card-title" v-html="highlightKeyword(card.title)"></h5>
                    <p class="card-text" v-html="highlightKeyword(card.paragraph)"></p>
                    <p class="card-text">
                    <small class="text-muted">{{ card.date }}</small>
                    </p>
                </div>
        </div>
      </div>
  
      <div v-else>
        <p>No cards found.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CardComponent',
    data() {
      return {
        searchQuery: '',
        cards: [
          { title: "Card 1", paragraph: "Vue.js is a versatile JavaScript framework.", date: "2024-09-10" },
          { title: "Card 2", paragraph: "Vue.js components make development easy.", date: "2024-09-11" },
          { title: "Card 3", paragraph: "Use Vue Router for SPA navigation.", date: "2024-09-12" },
          { title: "Card 4", paragraph: "Vuex provides a state management solution.", date: "2024-09-13" },
          { title: "Card 5", paragraph: "Composition API offers more flexibility.", date: "2024-09-14" },
          { title: "Card 6", paragraph: "Vue.js supports event handling.", date: "2024-09-15" },
          { title: "Card 7", paragraph: "Vue's ecosystem is rich and diverse.", date: "2024-09-16" },
          { title: "Card 8", paragraph: "Vue is perfect for building reactive UIs.", date: "2024-09-17" },
          { title: "Card 9", paragraph: "Use props for communication between components.", date: "2024-09-18" },
          { title: "Card 10", paragraph: "Vue.js provides a clean and simple API.", date: "2024-09-19" }
        ],
        filteredCards: [],
      };
    },
    created() {
      this.filteredCards = this.cards;
    },
    methods: {
      filterCards() {
        const query = this.searchQuery.toLowerCase();
        this.filteredCards = this.cards.filter(card => {
          return (
            card.title.toLowerCase().includes(query) || 
            card.paragraph.toLowerCase().includes(query)
          );
        });
      },
      highlightKeyword(text) {
        if (!this.searchQuery) return text;
        const regex = new RegExp(`(${this.searchQuery})`, 'gi');
        return text.replace(regex, '<mark>$1</mark>');
      }
    }
  };
  </script>
  
  <style >
  .card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 16px;
    margin: 8px;
  }
  input {
    margin-bottom: 20px;
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
  }
  mark {
    background-color: yellow;
    font-weight: bold;
  }
  </style>
  