<template>
  <b-modal
    ref="modal"
    id="glassWallModal"
    hide-header
    hide-footer
    v-model="modalVisibility"
    size="lg"
    class="modal-container glass-wall-modal"
    @hide="pause()"
    @show="play()"
  >
    <video
      controls="controls"
      class="responsive-img glass-wall-modal-video"
      ref="video"
    >
      <source type="video/mp4" :src="video.src" />
    </video>
  </b-modal>
</template>

<script>
export default {
  name: 'GlassWallModal',
  props: {
    modalShow: {
      type: Boolean,
      default: () => false
    },
    videoName: {
      type: String,
      default: () => ''
    }
  },
  data () {
    return {
      modalVisibility: false,
      options: {
        slidesToShow: 3,
        arrows: true,
        infinite: true,
        accessibility: true,
        adaptiveHeight: true,
        edgeFriction: 0.30,
        swipe: true,
        centerMode: true,
        prevArrow: '<div class="slider-arrow slider-prev"></div>',
        nextArrow: '<div class="slider-arrow slider-next"></div>'
      }
    }
  },
  watch: {
    modalShow: function () {
      this.modalVisibility = this.modalShow
    }
  },
  computed: {
    video () {
      return {
        src: require(`~/assets/video/${this.videoName}`)
      }
    }
  },
  methods: {
    pause () {
      if (this.videoName) {
        this.$refs.video.pause()
      }
      this.$emit('hide')
    },
    play () {
      if (this.videoName) {
        this.$nextTick(() => {
          this.$refs.video.play()
        })
      }
    }
  }
}
</script>
<style lang="scss">
#glassWallModal{
  .modal-dialog {
    -webkit-transform: none !important;
    transform: none !important;
    margin: auto !important;
    top: 50% !important;
    -ms-transform: translateY(-50%) !important;
    transform: translateY(-50%) !important;
  }
}

</style>
