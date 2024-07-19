<template>
  <q-page class="bg-grey-4 column">
   <h4>ToDo-List</h4>
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
      this.tasks.splice(index, 1);
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