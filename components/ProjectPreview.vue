<template>
  <div class="project-cover" @click="onClick">
    <div class="project-data">
      <div class="project-title">
        {{ title }}
      </div>
      <div class="project-icon">
        {{ icon }}
      </div>
    </div>
    <img :src="imagePath" alt="" />
  </div>
</template>

<script>
  export default {
    computed: {
      imagePath () {
        return require('assets/' + this.thumb + '.jpg')
      },
      icon () {
        if (this.projectType === 'graphic') {
          return 'G'
        } else if (this.projectType === 'video') {
          return 'V'
        }
      }
    },
    methods: {
      onClick () {
        this.$router.push({ path: this.path })
      }
    },
    props: {
      title: {
        type: String
      },
      projectType: {
        type: String
      },
      path: {
        type: String
      },
      thumb: {
        type: String,
        required: true
      }
    }
  }
</script>

<style lang="scss" scoped>
  $white: #EFEFEF;
  $black: #35495e;
  $project-spacing: 5px;

  .project-data {
    color: $white;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    align-items: center;
    overflow: hidden;
    background-color: rgba($black, 0);
    margin-bottom: 4px; // Magic number...
    padding-left: 10px;
    padding-right: 10px;

    transition-duration: .2s;
    transition-property: background-color;
    transition-timing-function: ease-in-out;
  }

  .project-title {
    font-size: 30px;
    text-align: center;
    transform: translateY(-100%);
    opacity: 0;
    width: 100%;

    transition-duration: .2s;
    transition-property: transform opacity;
    transition-timing-function: ease-in-out;
  }

  .project-icon {
    font-size: 30px;
    align-self: flex-end;
    position: absolute;
    right: -10px;
    bottom: 10px;
    opacity: 0;

    transition-duration: .2s;
    transition-property: right opacity;
    transition-timing-function: ease-in-out;
  }

  .project-cover {
    display: block;
    flex: 0 0 auto;
    // padding: $project-spacing;
    position: relative;
    border: solid $white $project-spacing;
    margin-bottom: -4px; // Magic number...

    img {
      max-width: 100%;
      max-height: 100%;
      transition-duration: .2s;
      transition-property: filter;
      transition-timing-function: ease-in-out;
    }

    &:hover {
      cursor: pointer;

      .project-title {
        transform: translateX(0);
        opacity: 1;
      }

      .project-icon {
        right: 10px;
        opacity: 1;
      }

      .project-data {
        background-color: rgba($black, 0.7);
      }
    }

    @media (min-width: 1401px) {
      height: calc(100%/6);
      width: calc(100%/6);
    }

    @media (min-width: 1201px) and (max-width: 1400px) {
      height: calc(100%/5);
      width: calc(100%/5);
    }

    @media (min-width: 1001px) and (max-width: 1200px) {
      height: calc(100%/4);
      width: calc(100%/4);
    }

    @media (min-width: 801px) and (max-width: 1000px) {
      height: calc(100%/3);
      width: calc(100%/3);
    }

    @media (min-width: 601px) and (max-width: 800px) {
      height: calc(100%/2);
      width: calc(100%/2);
    }

    @media (max-width: 600px) {
      height: calc(100%);
      width: calc(100%);
    }
  }
</style>
