<template>
  <div>
    <div class="picklizr__title" v-html="'PICKLIZR'"></div>
    <div class="picklizr__grid">
      <div class="grid__box arrow-top-left"></div>
      <div class="grid__box top" v-html="people[3].name" :style="{backgroundColor: people[3].color}"></div>
      <div class="grid__box arrow-top-right"></div>
      <div class="grid__box left" v-html="people[0].name" :style="{backgroundColor: people[0].color}"></div>
      <div class="grid__box center" v-html="nick.name" :style="{backgroundColor: nick.color}"></div>
      <div class="grid__box right" v-html="people[2].name" :style="{backgroundColor: people[2].color}"></div>
      <div class="grid__box arrow-bottom-left"></div>
      <div class="grid__box bottom" v-html="people[1].name" :style="{backgroundColor: people[1].color}"></div>
      <div class="grid__box arrow-bottom-right"></div>
    </div>
    <div class="button__container">
      <div class="button" v-html="'Picklize'" v-on:click="picklize"></div>
    </div>
  </div>
</template>

<script>
  /* eslint-disable indent */

  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    data () {
      return {
        nick: {
          name: 'Nick',
          color: 'red'
        },
        people: [
          {
            id: 0,
            name: 'Linda',
            isEditing: 2,
            color: 'green'
          },
          {
            id: 1,
            name: 'Josh',
            isEditing: 3,
            color: 'blue'
          },
          {
            id: 2,
            name: 'Eric',
            isEditing: 4,
            color: 'yellow'
          },
          {
            id: 3,
            name: 'Id',
            isEditing: 1,
            color: 'purple'
          }
        ]
      }
    },
    methods: {
      picklize () {
        let array = [0, 1, 2, 3]
        let shuffleArray = this.shuffle(array)

        let organizedPeople = this.people.map((person, index) => {
          while (person.isEditing === shuffleArray[index] || person.id === shuffleArray[index]) {
            shuffleArray = this.shuffle(shuffleArray)
          }
          person.isEditing = shuffleArray[index]
          return person
        }).sort((a, b) => a.isEditing - b.isEditing)

        this.people = organizedPeople
      },
      shuffle (array) {
        let currentIndex = array.length
        let tempValue, randomIndex

        while (currentIndex !== 0) {
          randomIndex = Math.floor(Math.random() * currentIndex)
          currentIndex--

          tempValue = array[currentIndex]
          array[currentIndex] = array[randomIndex]
          array[randomIndex] = tempValue
        }
        return array
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .picklizr {
    &__title {
      text-align: center;
      font-size: 20px;
    }

    &__grid {
      display: grid;
      grid-template: "arrow-top-left top arrow-top-right" "left center right" "arrow-bottom-left bottom arrow-bottom-right";

      .grid {
        &__box {
          border: solid 1px;
          height: 150px;
          transition: background-color 1s ease-in-out;
        }
      }

      .center {
        background-image: url('../assets/pickle.png');
        background-size: cover;
      }
    }
  }

  .button {
    &__container {
      display: flex;
      justify-content: center;
      width: 100%;
    }

    height: 50px;
    padding: 5px 10px;
    background-color: lightblue;
    border-radius: 6px;
  }

</style>
