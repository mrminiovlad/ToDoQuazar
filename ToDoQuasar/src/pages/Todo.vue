<template>
  <q-page class="bg-grey-4 column">
   <h4 class="q-pa-lg">ToDo-List</h4>
   <div class="row q-pa-sm bg-grey">
    <q-input  @keyup.enter="addTask" filled class="col" square bg-color="white" v-model="NewTask"  placeholder="add task" dense>
       
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>
      </q-input>
   </div>
   <q-list separator bordered>
      <q-item @click="task.done= !task.done" clickable :class="{ 'done bg-green-3': task.done}"
      v-for="(task, index) in tasks" :key="task.title"  v-ripple>
        <q-item-section avatar>
          <q-checkbox class="no-pointer-events" v-model="task.done" val="teal" color="teal" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn @click.stop="DeleteTask(index)"
           flat round color="grey" icon="delete" />
        </q-item-section>
      </q-item>

      
    </q-list>
  </q-page>
</template>

<script>
export default {
  data(){
    return{
      NewTask: "",
    tasks:[
        {title: "Hi",
        done: false,
      },
      {title: "Привет",
        done: false,
      },
      {title: "Bonjour",
        done: false,
      },
      ],
    };
  },
  methods:{
    DeleteTask(index){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Точно эта задача больше не нужна?',
        cancel: true,
        persistent: true,
      })
      .onOk(() => {
        this.tasks.splice(index, 1);
        this.$q.notify("deleted"); 
      });
    },
    addTask(){
      this.tasks.push({
        title: this.NewTask,
        done: false
      });
      this.NewTask = "";
    },
  },
};
</script>

<style lang="scss">
.done{
  .q-item__label{
    text-decoration: line-through;
    color: teal;
  }
}
</style>