<template>
  <div class="seat-container">
    <div v-for="row in rowNumber" :key="row" class="seat-row" :class="{ 'no-spacer': row === 11 }">
      <template v-if="row < 10">
        <template v-for="column in columnNumber">
          <div
            :key="column"
            class="seat-column"
            :class="selectedSeats.includes(seatNumber(row, column)) ? 'not-available' : 'available'"
            @click="selectSeat(row, column)">
            <div class="seat-number">{{ seatNumber(row, column) }}</div>
          </div>
        </template>
      </template>
      <template v-else-if="row == 10">
        <template v-for="blank in 2">
          <div :key="blank" class="seat-column blank"></div>
        </template>
        <template v-for="column in (columnNumber - 2)">
          <div
            :key="column + 2"
            class="seat-column" 
            :class="selectedSeats.includes(seatNumber(row, column)) ? 'not-available' : 'available'"
            @click="selectSeat(row, column)">
            <div class="seat-number">{{ seatNumber(row, column) }}</div>
          </div>
        </template>
      </template>
      <template v-if="row === 11">
        <template v-for="column in (columnNumber + 1)">
          <div
            :key="column"
            class="seat-column"
            :class="selectedSeats.includes(seatNumber(row, column)) ? 'not-available' : 'available'"
            @click="selectSeat(row, column)">
            <div class="seat-number">{{ seatNumber(row, column) }}</div>
          </div>
        </template>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BusSeat',

  data () {
    return {
      rowNumber: 11,
      columnNumber: 5,
      selectedSeats: []
    }
  },

  methods: {
    seatNumber (row, column) {
      return (row - 1) * 5 + column
    },
    selectSeat (row, column) {
      const number = this.seatNumber(row, column)
      const index = this.selectedSeats.indexOf(number)

      if (index < 0) {
        this.selectedSeats.push(number)
      } else {
        this.selectedSeats.splice(index, 1)
      }
    }
  }
}
</script>
