<!-- Hier steht unser Template für unsere Komponente -->
<template>
  <li>
    <h2>{{ name }}</h2>
    <h3>{{ isMyFavorite ? ' **Sponsored by NordVPN**' : ''}}</h3>
    <button @click='toggleDetails'>Details</button>
    <button  @click='toggleFavorite'>Toggle Favorite</button>
    <button @click='deleteContact'>Delete</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }} 
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  // props können als array angegeben werden
  // props: ['name','phoneNumber','emailAddress','isFavorite'],

  // props können als Objekte mit speziellen Eigenschaften angegeben werden
  props: {
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true
    },
    emailAddress: {
      type: String,
      required: true
    },
    isFavorite: {
      type: String,
      required: false,
      default: '0',
      // Es kann auch ein validator angegeben werden
      // hier wird einfach überprüft, ob '1' oder '0' übergeben wurde
      validator: function(value) {
        return value=== '1' || value === '0';
      }
    }
  },
  
  
  data() {
    return {
      detailsAreVisible: false,
      isMyFavorite: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
      console.log(this.phoneNumber);
    },
    toggleFavorite() {
      this.isMyFavorite = !this.isMyFavorite
    },
      deleteContact() {
        // Index im Array suchen
      const index = this.$parent.friends.findIndex(
        (friend) => friend.name === this.name
      );
        // Überprüfen ob es den Index gibt
      if (index !== -1) {
        // Löschen des Kontakts
        this.$parent.friends.splice(index, 1);
      }
      }
    
  }
};
</script>