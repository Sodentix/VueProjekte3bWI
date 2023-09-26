<template>
  <section>
    <div class="headlines">
     <h1 id="headline">Create Tasks</h1>
    <h1 id="headline2">Task-Overview</h1>
    </div>


    <div class="container">

    <div class="menu">
    <div>
    <input type="text" class="inputFields" id="nameInput" maxlength="30" placeholder="Enter task-name...">
    </div>
    <div>
    <input type="text" class="inputFields" id="descriptionInput" placeholder="Enter description...">
    </div>
    <div>
    <input type="date" class="inputFields" id="dateInput" placeholder="Enter due-date...">
    <button @click="addTask" id="addButton">Add</button>
    </div>

    </div>


    <div class="TaskDiv">
    
    <ul>
      <to-do-list
        v-for="task in tasks"
        :key="task.id"
        :taskName="task.name"
        :taskDescription="task.description"
        :duedate="task.duedate"
        :isFavorite="task.isFavorite"
      ></to-do-list>
    </ul>
    </div>
    </div>
  </section>
</template>

<script>
import ToDoList from "./components/ToDoList.vue";

export default {
  components: {
    ToDoList,
  },
  data() {
    return {
      tasks: [
        {
          id: "manuel",
          name: "Test-Aufgabe",
          description: "Test-Beschreibung",
          duedate: "2315-03-21",
          isFavorite: "1",
        },
      ],
    };
   
  },

  created() {
    // Daten aus dem Local Storage laden, wenn die Komponente erstellt wurde
    this.loadFromLocalStorage();
  },

   methods: {
    addTask() {
     if(document.getElementById('nameInput').value == "")
     {
         alert("Please enter a task name!")
     }
     else {
      this.tasks.push(
        {id: this.tasks.length,
        name: document.getElementById('nameInput').value,
        description: document.getElementById('descriptionInput').value,
        duedate: document.getElementById('dateInput').value,
        isFavorite: "0"})
        document.getElementById('nameInput').value = null;
        document.getElementById('descriptionInput').value = null;
        document.getElementById('dateInput').value = null;
         this.saveToLocalStorage();
     }

    
    },
    
    saveToLocalStorage() {
      // Daten speichern
     localStorage.setItem('taskData', JSON.stringify(this.tasks))
    },

    loadFromLocalStorage() {
      // Daten laden
      const data = localStorage.getItem('taskData')
      if (data) {
        this.tasks = JSON.parse(data)
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
  background: rgb(2,0,36);
  background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(9,62,121,1) 0%, rgba(0,212,255,1) 100%);
}

.headlines {
  display: flex;
  flex-direction: row;
}
#headline {
  border-bottom: white 1px solid;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  color: whitesmoke;
  width: 35%; /* Neues Attribut für die Breitenanpassung */
  padding: 0.5rem 1rem;
  margin-left: 1rem;
  
}

#headline2 {
  border-bottom: white 1px solid;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  color: whitesmoke;
   /* Neues Attribut für die Breitenanpassung */
  padding: 0.5rem 1rem;
  margin-left: 2rem;
  margin-right: 1rem;
  width: 58rem;
}

.container {
  display: flex;
}

.menu {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-left: 1rem;
  padding-top: 10px;
  width: 35%;
  
}

.menu > div:first-child * {
  background-color: lightgrey;
  border: 2px solid rgb(0, 0, 0);
  border-radius: 2px;
  width: 100%;
  padding-bottom: 3rem;
}

.menu > div:nth-child(2) * {
  background-color: lightgrey;
  border: 2px solid rgb(0, 0, 0);
  border-radius: 2px;
  width: 100%;
  padding-bottom: 8rem;
  
}

.menu > div:nth-child(3) * {
  border: 2px solid rgb(0, 0, 0);
  border-radius: 2px;
  height: 2rem;
  
}

.menu > div:nth-child(3) {
  display: flex;
  flex-direction: row;
  gap: 5rem;
  text-align: center;
 
}

#addButton {
  color: white;
  width: 25rem;
  background-color: rgb(4, 8, 241);
  text-align: center;
  font-size: 1rem;
}



.generalButtons {
  font: inherit;
  cursor: pointer;
  border: 1px solid #080808;
  background-color: #023e8a;
  color: white;
  margin-left: 1rem;
  height: 2rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
  transition: background-color 0.4s ease;
}

#app button:hover,
#app button:active {
background-color: rgb(4, 8, 241);
}


.checkboxID {
  width: 30px;
  margin-left: 0rem;
  margin-right: 1rem;
  margin-top: 0.1rem;
  
}

input[type="checkbox"]:checked {
  background-color: green;
}

.TaskDiv {
  width: 65%;
}


header {
  box-shadow: 0 2px 8px rgba(82, 78, 78, 0.26);
  margin: 3rem auto;
  border-radius: 2px;
  padding: 1rem;
  background-color: rgb(19, 16, 16);
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

header .inputFields {
  margin-right: 20px;
}

#headerText {
color: white;
}


.taskName {
color: rgb(55, 59, 59);
}


.taskHeader {
display: flex;
justify-content: space-around;
text-align: left;
padding-left: 1rem;
padding-right: 1rem;
}

li {
  list-style-type: none;
  background-color: #ade8f4;
  margin-right: 1rem;
  
}

li ul{
  padding-left: 1rem;
}

ul {
  margin-bottom: 2rem;
  padding-bottom: 0.5rem;
}
.task {
display: flex;
justify-content: space-between;
flex-direction: row;
background-color: #ade8f4;
margin-right: 1rem;
border-radius: 2px;
border-bottom: rgb(0, 0, 0) solid 1px;
}

.taskButtons {
display: flex;
justify-content: space-between;
padding-top: 1rem;
padding-left: 1rem;
padding-right: 1rem;
}







</style>