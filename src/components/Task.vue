<template>
    <!-- Card da tarefa -->
    <v-card class="mb-3 grey lighten-1 mx-2 px-2 py-2" width="100%">
        <v-col cols="12">
            <v-row class="d-flex align-center">
                <h5>{{task.name}}</h5>
                <v-spacer></v-spacer>
                <v-btn fab text dark x-small color="black">
                    <v-icon dark>
                    mdi-dots-vertical
                    </v-icon>
                </v-btn>
            </v-row>
        </v-col>
    </v-card>
    <!-- Fim do Card da tarefa -->
</template>

<script>
export default {
    props: {
        task: Object
    },
    data: () => ({
        
    }),
    watch:{
        task(val){
            console.log(val);
            return val;
        }
    }
};
</script>
