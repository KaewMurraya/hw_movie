<template>
    <div class="box">
        <template v-for="s in seats">
          <button
          :class="className(s)"
          :disabled="s.seated"
          @click="chooseSeat(s)"
          > {{s.id}} {{s.price}} </button>
          <span>&nbsp;</span>
        </template>
    </div>
</template>

<script>
import movie from 'Others/movie.json'
export default {
    props: [ 'movieId', 'selectSeats' ],
    methods: {
      className(seat) {
        const ids = this.selectSeats.map(s => s.id)
        const idx = ids.indexOf(seat.id)
        return [
          'button',
          { 'is-danger': seat.seated, 'is-primary': idx != -1 }
        ]
      },
      chooseSeat(seat) {
        this.$emit('chooseSeat', seat)
      }
    },
    computed: {
      seats() {
        return movie[this.movieId]
      }
    }
}
</script>
