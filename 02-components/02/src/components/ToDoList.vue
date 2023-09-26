<template>
  <li>
    <div class="task">
      <div class="taskHeader">
        <input type="checkbox" class="checkboxID" :checked="isChecked" @change="checkCheckbox">
        <h2 class="taskName">{{ taskName }}</h2>
      </div>
      
      <div class="taskButtons">
        <button @click="toggleDetails" class="generalButtons">Details</button>
        <button @click="removeTask" class="generalButtons">Remove</button>
      </div>
    </div>
    <h3>{{ isMyFavorite ? ' **Sponsored by NordVPN**' : ''}}</h3>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Description:</strong>
        {{ taskDescription }}
      </li>
      <li>
        <strong>Due-date:</strong>
        {{ duedate }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  props: {
    taskName: {
      type: String,
      required: true,
    },
    taskDescription: {
      type: String,
      required: true,
    },
    duedate: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: String,
      required: false,
      default: '0',
      // Es kann auch ein validator angegeben werden
      // hier wird einfach überprüft, ob '1' oder '0' übergeben wurde
      validator: function(value) {
        return value === '1' || value === '0';
      },
    },
  },
  data() {
    return {
      detailsAreVisible: false,
      isMyFavorite: false,
      isChecked: false,
    };
  },
  mounted() {
    // Beim Laden der Komponente den Checkbox-Status aus dem Local Storage abrufen
    const checkboxStatus = localStorage.getItem(this.taskName);
    if (checkboxStatus) {
      this.isChecked = checkboxStatus === 'true';
    }
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    checkCheckbox() {
      // Checkbox-Status umkehren
      this.isChecked = !this.isChecked;

      // Checkbox-Status im Local Storage speichern
      localStorage.setItem(this.taskName, this.isChecked.toString());
    },
    toggleFavorite() {
      this.isMyFavorite = !this.isMyFavorite;
    },
    removeTask() {
      // Index im Array suchen
      const index = this.$parent.tasks.findIndex((task) => task.name === this.taskName);
      // Überprüfen ob es den Index gibt
      if (index !== -1) {
        // Löschen der Aufgabe
        this.$parent.tasks.splice(index, 1);
        this.$parent.saveToLocalStorage();
      }
    },
  },
};
</script>
