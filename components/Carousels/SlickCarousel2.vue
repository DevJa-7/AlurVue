<template>
  <div class="carousel-center-focus">
    <component
      :is="slickComp"
      ref="slick"
      :options="options"
      @init="handleInit"
    >
      <slot name="content"></slot>
    </component>
  </div>
</template>

<script>
import '~/node_modules/slick-carousel/slick/slick.scss'
import '~/node_modules/slick-carousel/slick/slick-theme.scss'

export default {
  name: 'SlickCarousel2',

  components: {
    Slick: () => import('vue-slick')
  },

  props: {
    options: {
      type: Object,
      default: () => {}
    }
  },
  data () {
    return {
      slickComp: ''
    }
  },

  mounted: function () {
    this.$nextTick(function () {
      this.slickComp = 'Slick'
    })
  },

  methods:{
    handleInit:(e, slick) => {
      setTimeout(()=>{
        slick.slickSetOption("slidesToShow", slick.slickGetOption('slidesToShow'), true)
      }, 1000)
    }
  }
}
</script>
<style lang="scss">
@import '~/assets/styles/_variables.scss';
  .carousel-center-focus {
    width: 100%;
    .slick-slide {
      opacity: 0.6;
    }
    .slick-current {
      opacity: 1;
    }
    @media only screen and (max-width: 1008px){
      .slick-slide {
        opacity: 0.6;
      }
      .slick-current {
        opacity: 1;
      }
    }
  }
</style>
