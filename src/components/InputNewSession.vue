<template>
    <v-col cols="12">
        <v-row class="d-flex align-center px-2">
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
        </v-row>
    </v-col>
</template>

<script>
export default {
    data: () => ({
        show: false,
        message: 'Nova sessão',
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
        this.resetIcon()
        this.clearMessage()
      },
      clearMessage () {
        this.message = ''
      },
      resetIcon () {
        this.iconIndex = 0
      },
      changeIcon () {
        this.iconIndex === this.icons.length - 1
          ? this.iconIndex = 0
          : this.iconIndex++
      },
    },
};
</script>
