<template>
  <div>
        <button
          class="btn waves-effect"
          @click="actionButton"
          v-on:click="show = !show"
          :disabled="show"
          id="myButton"
        >
        <div id="divLoader">
          <span id="loading" v-if="show">
            <div class="preloader-wrapper small active">
              <div class="spinner-layer">
                <div class="circle-clipper left">
                  <div class="circle"></div>
                </div>
                <div class="gap-patch">
                  <div class="circle"></div>
                </div>
                <div class="circle-clipper right">
                  <div class="circle"></div>
                </div>
              </div>
            </div>
          </span>
        </div>
          <slot> Button</slot>
        </button> 
  </div>
</template>
<script>
export default {
  data() {
    return {
      show: false,
    };
  },
  methods: {
  },
};
</script>
<style>
.preloader-wrapper.small {
  width: 20px !important;
  height: 20px !important;
  margin-top: 8px;
}
#buttonText {
  vertical-align: top;
}
#divLoader{
  float:left;
  margin-right: 5px;
}
.spinner-layer{
  border-color: gray !important;
}

</style>
