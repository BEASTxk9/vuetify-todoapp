<template>
  <div class="home">

    <!-- add task input -->
       <v-text-field
       v-model="newTaskTitle"
       @click:append="addTask"
       @keyup.enter="addTask"
       class="pa-3"
            outlined
            label="Add Task"
            append-icon="mdi-plus-box"
            hide-details
            clearable
          ></v-text-field>
  
  <!-- list -->
  <v-list
      flat
      class="list"
    >
    <!-- for each item -->
    <div v-for="task in tasks" :key="task.id">

          <v-list-item
          class="pt-0"
          @click="doneTask(task.id)"
          :class="{'blue lighten-5' : task.done}"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{ 'text-decoration-line-through' : task.done}"
              >
                {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>

            <!-- delete btn -->
            <v-list-item-action>
          <v-btn 
          @click.stop="deleteTask(task.id)"
           icon
           >
            <v-icon color="primary lighten-1">mdi-delete-empty-outline</v-icon>
          </v-btn>
        </v-list-item-action>

          </template>

        </v-list-item>

        <v-divider></v-divider>

    </div>
    
   
    </v-list>
  </div>

</template>

<script>
  export default {
    name: 'Todo',
data(){
  return {
    newTaskTitle: '',
    tasks: [
      // {
      //   id: 1,
      //   title: 'Wake up.',
      //   done: false
      // },
      // {
      //   id: 2,
      //   title: 'Get food.',
      //   done: false
      // },
      // {
      //   id: 3,
      //   title: 'Eat food.',
      //   done: false
      // },
    ]
  }
},
methods: {
  addTask(){
    let newTask = {
      id: Date.now(),
      title: this.newTaskTitle,
      done: false
    }
    this.tasks.push(newTask)
    this.newTaskTitle = '';
console.log('Task Added Successfully');
  },
  doneTask(id) {
    // console.log('id: ', id);
    let task = this.tasks.filter(task => task.id == id)[0]
    task.done = !task.done
    // console.log(task);
  },
  deleteTask(id) {
    this.tasks = this.tasks.filter(task => task.id !== id)
    console.log('Task Deleted Successfully.')
  }
}
  }
</script>
