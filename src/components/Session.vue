<template>
    <v-col cols="12" sm="2">
        <v-sheet rounded="lg" color="grey lighten-2" outlined min-height="6vh" max-height="90.5vh">
        <v-col cols="12">
            <v-row class="d-flex align-center px-2 pt-1">
                <v-btn fab dark x-small color="indigo" class="mr-2" @click="newTask()" v-if="session.id == 1">
                    <v-icon dark>
                    mdi-plus
                    </v-icon>
                </v-btn>
                <h3>{{session.name}}</h3>
                <v-spacer></v-spacer>
                <v-btn fab text dark small color="indigo" @click="newSession()">
                    <v-icon dark>
                    mdi-cog
                    </v-icon>
                </v-btn>
            </v-row>
        </v-col>
        <v-col cols="12">
            <v-row>
                <v-card class="d-flex justify-center my-3 grey lighten-1 mx-2 py-2" width="100%" flat>
                    <h5>Sem tarefas no momento</h5>
                </v-card>
            </v-row>
        </v-col>
        </v-sheet>
    </v-col>
</template>

<script>
export default {
    props: {
        session: Object
    },
    data: () => ({
        //
    }),
};
</script>
