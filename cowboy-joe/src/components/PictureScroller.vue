<script>
export default {
  name: "PictureScroller",
  props: {
      currentDate: {
          type: Date,
          default: new Date()
      }
  },
  data() {
    return {
      firstQuarterImages: [
        require('../assets/NursingJoe.jpg'),
        require('../assets/ValentineJoe.jpg'),
        require('../assets/StPattyNurseJoe.jpg'),
        require('../assets/StPattyBichonJoe.jpg'),
      ],
      secondQuarterImages: [
          require('../assets/NursingJoe.jpg'),
          '../assets/EasterJoe.jpg',
          '../assets/HowBoutDemO\'sJoe.jpg',
          '../assets/EasterBunnyJoe.jpg',
      ],
      thirdQuarterImages: [
          '../assets/NursingJoe.jpg',
          '../assets/HappyMuricaDay.jpg',
          '../assets/doggoJoe.jpg',
          '../assets/SheriffJoe.jpg',
      ],
      fourthQuarterImages: [
          '../assets/NursingJoe.jpg',
          '../assets/SantaJoe.jpg',
          '../assets/ThanksgivingTurkey.jpg',
          '../assets/ChristmasJoe.jpg'
      ],
      timer: null,
      currentIndex: 0
    };
  },

  mounted: function() {
    this.startSlide();
  },

  methods: {
    startSlide: function() {
      this.timer = setInterval(this.next, 4000);
    },

    next: function() {
      this.currentIndex += 1;
    },
    prev: function() {
      this.currentIndex -= 1;
    }
  },

  computed: {
    currentImg() {
        
      return this.currentQuarter[Math.abs(this.currentIndex) % this.currentQuarter.length];
    },
    currentQuarter() {
        switch (this.currentDate.getMonth()) {
            case 0, 1, 2:
                return this.firstQuarterImages;
            case 3, 4, 5:
                return this.secondQuarterImages;
            case 6, 7, 8:
                return this.thirdQuarterImages;
            case 9, 10, 11:
                return this.thirdQuarterImages;
            default:
                return this.firstQuarterImages
        }
    }
  }
};
</script>

<template>
    <div>
        <transition-group name="fade" tag="div">
            <div v-for="i in [currentIndex]" :key="i">
                <img :src="currentImg" />
            </div>
        </transition-group>
        <a class="prev" @click="prev" href="#">&#10094; Previous</a>
        <a class="next" @click="next" href="#">&#10095; Next</a>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: all 5s ease;
  overflow: hidden;
  visibility: visible;
  position: absolute;
  width:100%;
  opacity: 1;
}

.fade-enter,
.fade-leave-to {
  visibility: hidden;
  width:100%;
  opacity: 0;
}

img {
  height:%;
  width:60%
}

.prev, .next {
  cursor: pointer;
  position: absolute;
  top: 40%;
  width: auto;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.7s ease;
  border-radius: 0 4px 4px 0;
  text-decoration: none;
  user-select: none;
}

.next {
  right: 0;
}

.prev {
  left: 0;
}

.prev:hover, .next:hover {
  background-color: rgba(0,0,0,0.9);
}
</style>