<template>
    <v-list
      class="pt-0"
      flat
    >

    <draggable
      v-model="tasks"
      handle=".handle">
      <task
          v-for="task in tasks"
          :key="task.id"
          :task="task"
      />
    </draggable>
        <!-- <div
          v-for="task in $store.state.tasks"
          :key="task.id"
        >
        <v-list-item
          @click="$store.commit('doneTask', task.id)"
          :class="{ 'blue lighten-5' : task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through' : task.done }"
              >{{ task.title }}</v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn
                @click.stop="$store.commit('deleteTask', task.id)" 
              icon>
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>

          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div> -->
    </v-list>
</template>

<script>
import draggable from "vuedraggable";
import Task from "@/components/Todo/Task.vue"
export default {
    data: () => ({

    }),
    methods: {

    },
    components: {
        'task': Task,
        draggable
    },
    computed: {
      tasks: {
        get() {
          return this.$store.getters.tasksFiltered;
        },
        set(value) {
          this.$store.dispatch('setTasks', value);
        }
      }
    }
}
</script>