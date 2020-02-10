<template>
  <div class="container">
    <div class="card-wrapper">
      <div id="card-1" class="card card--1"></div>
      <div id="card-2" class="card card--2"></div>
      <div id="card-3" class="card card--3"></div>
    </div>
    <input v-model="amount" type="number" />
    <button @click="amount = 0">0</button>
    <button @click="amount = 100">100</button>
    <button @click="amount = 200">200</button>
    <div id="section-1" class="section-1">
      <div id="mount-1" class="mount mount--1"></div>
      <div id="mount-2" class="mount mount--2"></div>
      <div id="mount-3" class="mount mount--3"></div>
      <div id="mount-4" class="mount mount--4"></div>
    </div>
    <div id="section-2" class="section-2">
      <div id="section-2-background" class="section-2-background"></div>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap'
export default {
  data() {
    return {
      amount: 0
    }
  },
  watch: {
    amount(newAmount, oldAmount) {
      console.log(newAmount, 'old was ' + oldAmount)
      if (this.amount >= 100 && this.amount < 200) {
        this.hideFirst()

        if (oldAmount >= 200) {
          this.restoreSecond()
        }
      }

      if (this.amount >= 200) {
        this.hideFirst()
        this.hideSecond()
      }

      if (oldAmount >= 100 && this.amount < 100) {
        if (oldAmount >= 200) {
          this.restoreAll()
        } else {
          this.restoreFirst()
        }
      }

      // if (oldAmount > 100) {
      //   gsap.to('#card-1', {
      //     duration: 1,
      //     opacity: 1,
      //     x: '0'
      //   })

      //   if (oldAmount > 200) {
      //     gsap.to('#card-2', {
      //       duration: 1,
      //       opacity: 1,
      //       x: '0'
      //     })
      //   }
      // }
    }
  },
  mounted() {
    // const timeline1 = gsap.timeline({
    //   defaults: { duration: 1, ease: 'power2' }
    // })
    // timeline1.add(gsap.to('#mount-1', { duration: 1, y: '-20px' }))
    // const tween = TweenMax.to('#mount-1', 1, { css: { left: '-100%' } })
    // console.log(tween)
    // .to('#mount-3', { duration: 1, y: '-30px' }, '-=1')
    // const startingPoint = 60
    const scene = this.$scrollmagic
      .scene({
        triggerElement: '#section-1',
        triggerHook: 0.5,
        duration: 1000
      })
      .setTween('#mount-1', {
        css: {
          top: '50px'
        }
      })

    const scene2 = this.$scrollmagic
      .scene({
        triggerElement: '#section-1',
        triggerHook: 0.5,
        duration: 1000
      })
      .setTween('#mount-2', {
        css: {
          top: '120px'
        }
      })

    const scene3 = this.$scrollmagic
      .scene({
        triggerElement: '#section-1',
        triggerHook: 0.5,
        duration: 1000
      })
      .setTween('#mount-4', {
        css: {
          top: '100px'
        }
      })

    const scene4 = this.$scrollmagic
      .scene({
        triggerElement: '#section-2',
        triggerHook: 0.5,
        duration: 1000
      })
      .setTween('#section-2-background', {
        css: {
          top: '0px'
        }
      })

    // scene
    //   .setTween(timeline1)
    //   .addIndicators()
    //   .addTo(controller)

    this.$scrollmagic.addScene(scene)
    this.$scrollmagic.addScene(scene2)
    this.$scrollmagic.addScene(scene3)
    this.$scrollmagic.addScene(scene4)
  },
  methods: {
    hideFirst() {
      const timeline = gsap.timeline({
        defaults: { duration: 1, ease: 'power3' }
      })
      timeline
        .to('#card-1', {
          opacity: 0,
          x: '-100px'
        })
        .to(
          '#card-2',
          {
            scale: 1
          },
          '-=1'
        )
        .to(
          '#card-3',
          {
            scale: 0.9
          },
          '-=1'
        )
    },
    hideSecond() {
      const timeline = gsap.timeline({
        defaults: { duration: 1, ease: 'power3' }
      })
      timeline
        .to('#card-2', {
          opacity: 0,
          x: '-100px'
        })
        .to(
          '#card-3',
          {
            scale: 1
          },
          '-=1'
        )
    },
    hideFirstAndSecond() {
      const timeline = gsap.timeline({
        defaults: { duration: 1, ease: 'power3' }
      })
      timeline
        .to('#card-2', {
          opacity: 0,
          x: '-100px'
        })
        .to(
          '#card-3',
          {
            scale: 1
          },
          '-=1'
        )
    },
    restoreFirst() {
      const timeline = gsap.timeline({
        defaults: { duration: 1, ease: 'power3' }
      })
      timeline
        .to('#card-1', {
          opacity: 1,
          x: '0'
        })
        .to(
          '#card-2',
          {
            scale: 0.9
          },
          '-=1'
        )
        .to(
          '#card-3',
          {
            scale: 0.8
          },
          '-=1'
        )
    },
    restoreSecond() {
      const timeline = gsap.timeline({
        defaults: { duration: 1, ease: 'power3' }
      })
      timeline
        .to('#card-2', {
          opacity: 1,
          x: '1rem'
        })
        .to(
          '#card-3',
          {
            scale: 0.9
          },
          '-=1'
        )
    },
    restoreAll() {
      const timeline = gsap.timeline({
        defaults: { duration: 1, ease: 'power3' }
      })
      timeline
        .to('#card-1', {
          opacity: 1,
          x: '0'
        })
        .to(
          '#card-2',
          {
            scale: 0.9,
            opacity: 1,
            x: '1rem'
          },
          '-=1'
        )
        .to(
          '#card-3',
          {
            scale: 0.8
          },
          '-=1'
        )
    }
  }
}
</script>

<style lang="scss" scoped>
.card-wrapper {
  position: relative;
  margin-top: 10rem;
  margin-left: 6rem;
  margin-bottom: 1rem;
  height: 300px;
}

.card {
  width: 100px;
  height: 300px;
  position: absolute;

  &--1 {
    background-color: aqua;
    z-index: 3;
  }

  &--2 {
    background-color: rgb(221, 112, 121);
    transform: translateX(1rem) scale(0.9);
    z-index: 2;
  }

  &--3 {
    background-color: #6d8cc3;
    transform: translateX(2rem) scale(0.8);
    z-index: 1;
  }
}

.section-1 {
  margin-top: 20rem;
  height: 100vh;
  width: 100%;
  background-color: rgb(153, 199, 252);
  position: relative;
}

.section-2 {
  height: 100vh;
  width: 100%;
  position: relative;
}

.section-2-background {
  position: absolute;
  top: 300px;
  left: 0;
  height: 100%;
  width: 100%;
  background: linear-gradient(white 10%, black);
}
.mount {
  position: absolute;
  width: 250px;
  height: 250px;
  border-right: 4px solid black;
  border-bottom: 4px solid black;
  transform: rotate(-135deg);
  top: 200px;
  left: 300px;
  background-color: rgb(153, 199, 252);

  &--1 {
    z-index: 2;
  }

  &--2 {
    left: 500px;
    top: 200px;
    z-index: 1;
  }

  &--3 {
    left: 700px;
    top: 150px;
    z-index: 2;
  }
  &--4 {
    left: 900px;
    top: 230px;
    z-index: 1;
  }
}
</style>
