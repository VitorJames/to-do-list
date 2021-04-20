<template>
    <v-col cols="12" sm="2">
        <v-sheet rounded="lg" color="grey lighten-1" min-height="90.5vh">
            <v-col cols="12">
                <v-row justify="center">
                    <h4 class="my-3">Relatório das tarefas</h4>
                </v-row>
            </v-col>
            <v-col cols="12">
                <v-row justify="center">
                    <!-- Card do relatório da sessão -->
                    <v-card color="grey lighten-2 mb-3" width="93%" v-for="(session,i) in sessions" :key="i">
                        <v-card-title class="pt-1 px-2">
                            <h5>{{session.name}}</h5>
                            <v-spacer></v-spacer>
                            <h5><span class="indigo--text">{{session.tasks.length}}</span>/{{tasks}}</h5>
                        </v-card-title>
                        <v-card-actions>
                            <v-col cols="12">
                                <v-row>
                                    <h6>{{percent(session.tasks.length)}}% de todas as tarefas</h6>
                                </v-row>
                                <v-row>
                                    <v-progress-linear
                                    :value="percent(session.tasks.length)"
                                    color="indigo"
                                    ></v-progress-linear>
                                </v-row>
                            </v-col>
                        </v-card-actions>
                    </v-card>
                    <!-- Fim Card do relatório da sessão -->
                </v-row>
            </v-col>
        </v-sheet>
    </v-col>
</template>

<script>
export default {
    props: {
        sessions: Array,
        tasks: Number
    },
    data: () => ({
        
    }),
    methods:{
        percent(tasks_session){
            var p = Math.round(parseInt(tasks_session)*100/parseInt(this.tasks));
            return isNaN(p) ? 0 : p;
        }
    }
};
</script>
