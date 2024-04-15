<template>
  <v-card class="pa-8 d-flex justify-center align-center flex-wrap h-screen" theme="dark">
    <v-container class="text-center">
      <v-row justify="center" dense>
        <v-col cols="12">
          <v-img
            class="mx-auto mt-12 mb-16"
            max-height="140"
            max-width="240"
            src="https://cdn.vuetifyjs.com/docs/images/logos/vuetify-logo-dark-text.svg"
          ></v-img>
          <!-- <h1 class="mx-auto mt-12 mb-16 text-uppercase">Belajar Vuetify</h1> -->
        </v-col>

        <v-col cols="12">
          <v-autocomplete
            :items="items"
            append-inner-icon="mdi-microphone"
            class="mx-auto"
            density="comfortable"
            menu-icon=""
            placeholder="Search Google or type a URL"
            prepend-inner-icon="mdi-magnify"
            style="max-width: 600px;"
            theme="light"
            variant="solo"
            auto-select-first
            item-props
            rounded
          ></v-autocomplete>
        </v-col>

        <v-col
          v-for="(shortcut, i) in shortcuts"
          :key="i"
          cols="auto"
        >
          <v-card
            :href="shortcut.href"
            class="pa-4"
            rel="noopener noreferer"
            target="_blank"
            width="112"
            flat
          >
            <v-avatar :icon="shortcut.icon" class="mb-2" color="white" variant="tonal"></v-avatar>

            <div class="text-caption text-truncate" v-text="shortcut.title"></div>
          </v-card>
        </v-col>

        <v-col cols="auto">
          <v-dialog v-model="dialog" max-width="500">
            <template v-slot:activator="{ props }">
              <v-card v-bind="props" class="pa-4" width="112" flat>

                <v-avatar class="mb-2" color="white" icon="mdi-plus" variant="tonal"></v-avatar>

                <div class="text-caption text-truncate">Add shortcut</div>
              </v-card>
            </template>

            <v-card rounded="lg" title="Add shortcut">
              <template v-slot:text>
                <v-label class="text-caption">Name</v-label>

                <v-text-field density="compact" variant="solo-filled" v-model="title" flat></v-text-field>
                <p class="text-red text-subtitle-1">
                  {{errors?.filter((e) => e.id === 'title')[0]?.title}}
                </p>
                
                <v-label class="text-caption">URL</v-label>

                <v-text-field density="compact" variant="solo-filled" v-model="href" flat></v-text-field>
                <p class="text-red text-subtitle-1">
                  {{errors?.filter((e) => e.id === 'href')[0]?.title}}
                </p>
              </template>

              <div class="py-4 px-5 text-end">
                <v-btn
                  class="text-none me-2"
                  color="blue"
                  text="Cancel"
                  variant="text"
                  border
                  @click="dialog = false"
                ></v-btn>

                <v-btn
                  class="text-none"
                  color="blue"
                  text="Done"
                  variant="flat"
                  @click="onSubmit"
                ></v-btn>
              </div>
            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      title: '',
      href: '',
      errors: [],
      items: [
        {
          prependIcon: 'mdi-clock-outline',
          title: 'recipe with chicken',
        },
        {
          prependIcon: 'mdi-clock-outline',
          title: 'best hiking trails near me',
        },
        {
          prependIcon: 'mdi-clock-outline',
          title: 'how to learn a new language',
        },
        {
          prependIcon: 'mdi-clock-outline',
          title: 'DIY home organization ideas',
        },
        {
          prependIcon: 'mdi-clock-outline',
          title: 'latest fashion trends',
        },
      ],
      shortcuts: [
        {
          icon: 'mdi-calendar',
          title: 'Date And Skeleton',
          href: '/date',
        }
  
      ],
    }),
    methods: {
      onSubmit() {

        if (!this.title) {
          if (!this.errors?.filter((e) => e.id === 'title').length > 0) {
            this.errors.push({
              id: 'title',
              title: 'Title harus ada'
            })
          }
        } else {
          this.errors = this.errors.filter((e) => e.id !== 'title');
        }

        if (!this.href) {
          if (!this.errors?.filter((e) => e.id === 'href').length > 0) {
            this.errors.push({
              id: 'href',
              title: 'Href harus ada'
            })
          }
        } else {
          this.errors = this.errors.filter((e) => e.id !== 'href');
        }

        // console.log(this.errors)

        if (this.href && this.title) {
          this.dialog = false;

          this.shortcuts.push({
            icon: 'mdi-material-ui',
            title: this.title,
            href: this.href
          })
        }
      }
    }
  }
</script>