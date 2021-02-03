<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <app-button
      @action="open"
      >
      {{ isNewsOpen ? 'Close' : 'Open' }}
    </app-button>
    <app-button color="danger"
            v-if="wasRead"
            @action="$emit('unmark', id)"
            >
      Отметить не прочитанной
    </app-button>
    <div v-if="isNewsOpen">
      <hr />
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias amet commodi dignissimos eveniet excepturi itaque minus, pariatur reiciendis rem voluptates?</p>
      <app-button
        color="primary"
        v-if="!wasRead"
        @action="mark"
      >Прочесть новость
      </app-button>
      <hr>
      <app-list></app-list>
    </div>
  </div>

</template>

<script>
import AppButton from '@/AppButton'
import AppList from '@/AppList'
export default {
  // props: ['title'],
  // emits: [ 'open-news' ],
  props: {
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator (value) {
        console.log(value)
        return true
      }
    },
    wasRead: {
      type: Boolean,
      required: true
    }
  },
  emits: {
    // 'open-news': null => если валидировать данные не нужно
    'open-news' (num) {
      if (num) {
        return true
      }
      console.warn('No data in open-news emit')
      return false
    },
    'read-news' (id) {
      if (id) {
        return true
      }
      console.warn('No data id for emit read-news')
      return false
    },
    unmark (id) {
      if (id) {
        return true
      }
      console.warn('No data id for emit unmark')
      return false
    }

  },
  data () {
    return {
      isNewsOpen: this.isOpen
    }
  },
  methods: {
    open () {
      this.isNewsOpen = !this.isNewsOpen
      if (this.isNewsOpen) {
        this.$emit('open-news', 42)
      }
    },
    mark () {
      this.isNewsOpen = false
      this.$emit('read-news', this.id)
    }
    // можем написать в одну строку прямо в шаблоне
    // unmark(){
    //   this.$emit('unmark', this.id)
    // }
  },
  components: {
    'app-button': AppButton,
    'app-list': AppList
  }
}
</script>

<style scoped>

</style>
