<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md q-gutter-sm">
      <q-btn color="primary" label="Select emoji" @click="emojiPickerDialog = true"/>
      <q-btn color="white" rounded size="256px" dense :label="selectedEmoji" @click="emojiPickerDialog = true"/>
    </div>

    <q-dialog v-model="emojiPickerDialog">
      <q-card>
        <q-card-section>
          <div class="text-h6">Selected: {{ selectedEmoji }}</div>
        </q-card-section>

        <q-card-section>
          <emoji-picker :data="emojiIndex" :emojiSize="24" :native="true" @select="selectEmoji"></emoji-picker>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn color="primary" label="OK" v-close-popup />
          <q-btn color="grey" label="Cancel" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

  </q-page>
</template>

<script>
import emojiData from 'emoji-mart-vue-fast/data/all'
import 'emoji-mart-vue-fast/css/emoji-mart.css'
import { Picker as EmojiPicker, EmojiIndex } from 'emoji-mart-vue-fast'

export default {
  name: 'PageIndex',
  data () {
    return {
      selectedEmoji: '',
      emojiPickerDialog: false
    }
  },

  components: {
    EmojiPicker
  },

  created () {
    this.emojiIndex = new EmojiIndex(emojiData)
  },

  methods: {
    selectEmoji (emoji) {
      this.selectedEmoji = emoji.native
    }
  }
}
</script>
