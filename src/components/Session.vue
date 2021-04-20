<template>
    <v-col cols="12" sm="2">
        <v-sheet rounded="lg" color="grey lighten-2" outlined min-height="6vh" max-height="90.5vh">
        <!-- Cabeçalho da sessão -->
        <v-col cols="12">
            <v-row class="d-flex align-center px-2 pt-1">
                <v-btn fab dark x-small color="indigo" class="mr-2" @click="newTask=true" v-if="session.id == 1">
                    <v-icon dark>
                    mdi-plus
                    </v-icon>
                </v-btn>
                <h3>{{session.name}}</h3>
                <v-spacer></v-spacer>
                <v-btn fab text dark small color="indigo">
                    <v-icon dark>
                    mdi-cog
                    </v-icon>
                </v-btn>
            </v-row>
        </v-col>
        <!-- Fim do Cabeçalho da sessão -->

        <!-- Botão de nova tarefa -->
        <v-col cols="12" class="pt-2 pb-0" v-if="session.id == 1 && newTask">
            <v-text-field
                v-model="message"
                :append-outer-icon="message ? 'mdi-content-save' : 'mdi-close'"
                clear-icon="mdi-close-circle"
                solo
                flat
                clearable
                type="text"
                class="pb-0 mb-0"
                @click:append="toggleMarker"
                @click:append-outer="saveSession"
                @click:clear="clearMessage"
            ></v-text-field>
        </v-col>
        <!-- Fim do Botão de nova tarefa -->
        <v-col cols="12" v-if="session.tasks.length == 0">
            <v-row>
                <v-card class="d-flex justify-center my-3 transparent mx-2 py-2" width="100%" flat>
                    <h5>Sem tarefas no momento</h5>
                </v-card>
            </v-row>
        </v-col>

        <!-- Tarefa -->
        <v-col cols="12" v-else>
            <v-row class="pt-4">
                <template v-for="(task,t) in session.tasks">
                    <Task :task="task" :key="t"/>
                </template>
            </v-row>
        </v-col>
        <!-- Fim da Tarefa -->
        </v-sheet>
    </v-col>
</template>

<script>
import Task from './Task';

export default {
    props:{
        session: Object,
    },
    components:{
        Task
    },
  data: () => ({
    newTask: false,
    message: 'Nova tarefa',
    marker: true,
    iconIndex: 0,
  }),

  computed: {
    icon () {
      return this.icons[this.iconIndex]
    },
  },

  methods: {
    toggleMarker () {
      this.marker = !this.marker
    },
    saveSession () {
      if (this.message == '') {
        this.newTask = false;
      } else {
        this.$emit('newTask',{
            id: this.session.tasks.length+1,
            name: this.message,
        });
        this.resetIcon()
        this.clearMessage()
        this.newTask = false;
      }
    },
    clearMessage () {
      this.message = 'Nova tarefa'
    },
    resetIcon () {
      this.iconIndex = 0
    },
  },
}
</script>
