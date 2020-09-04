<template>
  <div class="wrapper">
    <div class="left">
      <div class="up">
        <div
            class="blue"
            :class="{blueOpacity: opacityValue.blueOpacity}"
            @click="opacityOnClick('blueOpacity')"
        ></div>
        <div
            class="red"
            :class="{redOpacity: opacityValue.redOpacity}"
            @click="opacityOnClick('redOpacity')"
        ></div>
      </div>
      <div class="down">
        <div
            class="yellow"
            :class="{yellowOpacity: opacityValue.yellowOpacity}"
            @click="opacityOnClick('yellowOpacity')"
        ></div>
        <div
            class="green"
            :class="{greenOpacity: opacityValue.greenOpacity}"
            @click="opacityOnClick('greenOpacity')"
        ></div>
      </div>
    </div>
    <div class="right">
      <h1>Score: {{score}}</h1>
      <button v-if="!start" @click="startClick">Start</button>
      <button v-if="start" @click="restartClick">Restart</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "SimonGame",
  data() {
    return {
      score: 0,
      gameArray: [],
      playerArray: [],
      start: false,
      gameOver: false,
      baseParamColor: {
        1: "blueOpacity",
        2: "redOpacity",
        3: "yellowOpacity",
        4: "greenOpacity"
      },
      currentColor: "",
      opacityValue: {
        blueOpacity: false,
        redOpacity: false,
        yellowOpacity: false,
        greenOpacity: false,
      },
      easyLevel: 1500,
      mediumLevel: 1000,
      hardLevel: 400
    }
  },
  methods: {
    restartClick() {
      this.score = 0
      this.startClick()
    },
    startClick() {
      this.start = true
      this.gameArray.push(this.randomInteger(1, 4))
      this.startGameBot(this.mediumLevel)
    },
    randomInteger(min, max) {
      const rand = min - 0.5 + Math.random() * (max - min + 1)
      return Math.round(rand)
    },
    startGameBot(level) {
      this.gameArray.forEach((el, index) => {
        setTimeout(() => {
          this.currentColor = this.baseParamColor[el]
          this.opacityOnClick(this.currentColor)
        }, level * (index + 1))
      })
    },
    opacityOnClick(color, level = 200) {
      this.opacityValue[color] = true
      setTimeout(() => {
        this.opacityValue[color] = false
      }, level)
    }
  },
}
</script>

<style lang="scss">
  @mixin base-params {
    width: 300px;
    height: 300px;
    opacity: .1;
    margin: 20px;
    cursor: pointer;
    border: 0px solid;
    border-radius: 5px;
  }

  @mixin flex-row {
    display: flex;
    flex-direction: row;
    margin-top: 50px;
  }

  .wrapper {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    .left {

      .up {
        @include flex-row;

        .blue {
          background-color: blue;
          @include base-params;
        }

        .blueOpacity {
          opacity: 1;
        }

        .red {
          background-color: red;
          @include base-params;
        }

        .redOpacity {
          opacity: 1;
        }

      }

      .down {
        @include flex-row;

        .yellow {
          background-color: yellow;
          @include base-params;
        }

        .yellowOpacity {
          opacity: 1;
        }

        .green {
          background-color: green;
          @include base-params;
        }

        .greenOpacity {
          opacity: 1;
        }
      }

    }

    .right {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      h1 {
        font-size: 50px;
      }

      button {
        font-size: 40px;
        width: 200px;
        height: 200px;
        cursor: pointer;
      }
    }

  }

</style>