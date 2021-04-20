<template>
  <v-container class="mx-0">
    <v-row>
      <v-col cols="12">
        <v-row>
          <!-- Relatório de tarefas -->
          <Analytics :sessions="sessions" :tasks="tasks"/>
          <!-- Fim do relatório de tarefas -->

          <!-- Sessões -->
          <template v-for="(session,i) in sessions">
            <Session :session="session" @newTask="session.tasks.push($event);manageTasks();" :key="i"/>
          </template>
          <!-- Fim das Sessões -->

          <!-- Botão de nova sessão -->
          <v-col cols="12" sm="2" v-if="sessions.length <= 4">
            <v-sheet rounded="lg" min-height="6vh" class="d-flex align-center transparent" v-if="!newSession">
              <v-col cols="12">
                <v-row class="d-flex align-center px-2">
                  <v-btn fab dark small color="indigo" @click="newSession=true">
                    <v-icon dark>
                      mdi-plus
                    </v-icon>
                  </v-btn>
                </v-row>
              </v-col>
            </v-sheet>
            <v-sheet rounded="lg" min-height="6vh" class="d-flex align-center transparent pt-0" v-else>
              <v-col cols="12" class="px-0 pt-0">
                <v-text-field
                    v-model="message"
                    :append-outer-icon="message ? 'mdi-content-save' : 'mdi-close'"
                    clear-icon="mdi-close-circle"
                    solo
                    clearable
                    label=""
                    type="text"
                    @click:append="toggleMarker"
                    @click:append-outer="saveSession"
                    @click:clear="clearMessage"
                ></v-text-field>
              </v-col>
            </v-sheet>
          </v-col>
          <!-- Fim do Botão de nova sessão -->
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Analytics from './Analytics';
import Session from './Session';

export default {
  components: {
    Analytics,
    Session,
  },
  data: () => ({
    newSession: false,
    message: 'Nova sessão',
    marker: true,
    iconIndex: 0,
    sessions: [
      {
        id: 1,
        name: 'A fazer',
        tasks: [],
      },
      {
        id: 2,
        name: 'Fazendo',
        tasks: [],
      },
      {
        id: 3,
        name: 'Feito',
        tasks: [],
      },
    ],
    tasks: 0
  }),
  computed: {
    icon () {
      return this.icons[this.iconIndex]
    },
  },
  watch:{
    sessions(data){
      this.manageTasks();
      return data;
    }
  },
  methods: {
    toggleMarker () {
      this.marker = !this.marker
    },
    saveSession () {
      if (this.message == '') {
        this.newSession = false;
      } else {
        this.sessions.push({
          id: this.sessions.length+1,
          name: this.message,
          tasks: []
        });
        this.resetIcon()
        this.clearMessage()
        this.newSession = false;
      }
    },
    clearMessage () {
      this.message = 'Nova sessão'
    },
    resetIcon () {
      this.iconIndex = 0
    },
    manageTasks () {
      var count = 0;
      this.sessions.map((session) => {
        count += session.tasks.length ;
      });
      this.tasks = count;
    }
  },
}
</script>
