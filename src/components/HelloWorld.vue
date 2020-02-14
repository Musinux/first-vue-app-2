<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
    <v-card
      class="mx-auto"
      max-width="400"
      tile
    >
      <v-form v-model="valid">
        <v-container>
          <v-row>
            <v-col
              cols="12"
              md="12"
            >
              <v-text-field
                v-model="title"
                :rules="titleRules"
                label="Title"
                required
              ></v-text-field>
            </v-col>

            <v-col
              cols="12"
              md="12"
            >
              <v-textarea
                v-model="content"
                label="Content"
                required
              ></v-textarea>
            </v-col>
            <v-col class="text-center" cols="12" sm="4">
              <div class="my-2">
                <v-btn color="primary"
                  @click="buttonClicked"
                >Send</v-btn>
              </div>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </v-card>
      <v-container>
        <v-layout
          text-center
          wrap
        >
          <v-card
            class="mx-auto"
            max-width="400"
            tile
          >
            <v-list-item two-line v-for="(item, idx) in todos" :key="item.id">
              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
                <v-list-item-subtitle>{{ item.content }}</v-list-item-subtitle>
                <v-btn @click="deleteElement(idx)">Delete</v-btn>
              </v-list-item-content>
            </v-list-item>
            <p v-if="state === true">Blablabla</p>
            <button @click="state = !state">Click !</button>
          </v-card>
        </v-layout>
      </v-container>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',

  data: () => ({
    state: false,
    valid: false,
    title: '',
    content: '',
    todos: [],
    titleRules: [
      v => !!v || 'Name is required',
      v => v !== 'Louis' || 'Louis is forbidden'
    ]
  }),
  methods: {
    buttonClicked () {
      if (!this.valid) return
      console.log('the button is clicked', this.title, this.content)

      let id
      if (this.todos.length) {
        id = this.todos[this.todos.length - 1].id + 1
      } else {
        id = 0
      }
      this.todos.push({
        id,
        title: this.title,
        content: this.content
      })
      console.log('todos',
        JSON.parse(JSON.stringify(this.todos)))
    },
    deleteElement (index) {
      this.todos.splice(index, 1)
    }
  }
}
</script>
