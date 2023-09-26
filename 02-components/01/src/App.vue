<template>
  <section>
    <header>
      <h1>My Friends</h1>
       <p class="headerText">Add a new friend</p>
    <input type="text" class="inputFields" id="nameInput" placeholder="Enter name...">
    <input type="number" class="inputFields" id="phoneInput" placeholder="Enter phone-number...">
    <input type="email" class="inputFields" id="mailInput" placeholder="Enter email-address...">
    <button @click="addContact" id="addButton">Add</button>
    <br>
    <br>
    <button @click="saveToLocalStorage">Daten speichern</button>
    <button @click="loadFromLocalStorage">Daten lesen</button>
    <button @click="deleteFriendData">Daten löschen</button>
    </header>
    <ul>
      <friend-contact
        name="Max Muster"
        phone-number="0123 456 789"
        email-address="manuel@test.com"
      ></friend-contact>
      <friend-contact
        name="Johannes Wegeler"
        phone-number="4567 890 123"
        email-address="julie@test.com"
      ></friend-contact>
      <friend-contact
        name="Julia Roberts"
        phone-number="3456 789 312"
        email-address="paolo@test.com"
      ></friend-contact> 
       <friend-contact
        name="Mathematikprofi Mag. Prof. Klaus Geismayr"
        phone-number="3456 789 312"
        email-address="paolo@test.com"
      ></friend-contact> 
    </ul>



    <header>
      <h1>Liste mit vfor</h1>
    </header>
   
    <ul>
      <friend-contact
        v-for="friend in friends"
        :key="friend.id"
        :name="friend.name"
        :phoneNumber="friend.phone"
        :emailAddress="friend.email"
        :isFavorite="friend.isFavorite"
      ></friend-contact>
    </ul>
  </section>
</template>

// ***************************************************************************
// Aufgaben:  1. toggleFavorite als Event in FriendContact einbauen
//            2. deleteContact in FriendContact einbauen
              3. Übung für Schüler: Eigene Komponente NewFriend.vue erstellen
// ***************************************************************************
<script>
import FriendContact from "./components/FriendContact.vue";

export default {
  components: {
    FriendContact,
  },
  data() {
    return {
      friends: [
        {
          id: "manuel",
          name: "Manuel Lorenz",
          phone: "0123 45678 90",
          email: "manuel@localhost.com",
          isFavorite: "1",
        },
        {
          id: "julie",
          name: "Julie Jones",
          phone: "0987 654421 21",
          email: "julie@localhost.com",
          isFavorite: "0",
        },
        {
          id: "Antonio",
          name: "Antonio Conte",
          phone: "3212 213 456",
          email: "antonio@localhost.com",
          isFavorite: "0",
        },
      ],
    };
   
  },
   methods: {
    addContact() {
      this.friends.push(
        {id: this.friends.length,
        name: document.getElementById('nameInput').value,
        phone: document.getElementById('phoneInput').value,
        email: document.getElementById('mailInput').value,
        isFavorite: "0"})
        
        document.getElementById('nameInput').value = null;
        document.getElementById('phoneInput').value = null;
        document.getElementById('mailInput').value = null;
    },

    saveToLocalStorage() {
      // Daten speichern
     localStorage.setItem('friendsData', JSON.stringify(this.friends))
    },

    deleteFriendData() {
      //Daten löschen
      this.friends = []; 
    },

    loadFromLocalStorage() {
      // Daten laden
      const data = localStorage.getItem('friendsData')
      if (data) {
        this.friends = JSON.parse(data)
      }
      
    }
    }
};
</script>



<style>
* {
  box-sizing: border-box;
}
html {
  font-family: "Jost", sans-serif;
}
body {
  margin: 0;
}
header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

header .inputFields {
  margin-right: 20px;
}

header .headerText {
color: white;
}
#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
#app li {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}
#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  margin-left: 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}
#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

#addButton {
  margin-top: 2vh;
}
</style>