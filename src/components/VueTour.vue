<template>
  <div>
    <button @click="$tours['myTour'].start()" class="btn btn-lg">Start the tour</button>
    <button @click="nextStep" class="btn btn-lg">Next step</button>
    <button @click="showLastStep" class="btn btn-lg">Show last step</button>
  </div>

  <v-tour name="myTour" :steps="steps" :callbacks="callbacks">
  </v-tour>
</template>

<script>
  export default {
    name: 'myTour',
    data() {
      return {
        steps: [
          {
            target: '#v-step-0',
            content: 'Dicover <strong>Vue Tour</strong>'
          },
          {
            target: '#v-step-1',
            header: {
              title: 'Vue Tour'
            },
            content: 'An awesome plugin made with Vue.js!'
          },
          {
            target: '#v-step-2',
            content: 'Try it, you\'ll love it!<br>You can put HTML in the steps and completely customize the DOM to suit your needs.',
            params: {
              placement: 'top'
            }
          },
          {
            target: '#v-step-3',
            content: 'てすとテストtest',
            params: {
              placement: 'left'
            }
          }
        ],
        callbacks: {
          onPreviousStep: this.myCustomPreviousStepCallback,
          onNextStep: this.myCustomNextStepCallback
        }
      }
    },
    mounted: function () {
      this.$tours['myTour'].start()
      this.callbacks.onStop = () => {
        document.querySelector('#v-step-0').scrollIntoView({vehavior: 'smooth'})
      }
    },
    methods: {
      nextStep () {
        this.$tours['myTour'].nextStep()
      },
      showLastStep () {
        this.$tours['myTour'].currentStep = this.steps.length = 1
      },
      myCustomPreviousStepCallback (currentStep) {
        console.log('[Vue Tour] A vustom previousStep callback has been called on step ' + (currentStep + 1))
      },
      myCustomNextStepCallback (currentStep) {
        console.log('[Vue Tour] A custom nextStep callback has been called on step ' + (currentStep + 1))

        if (currentStep === 1) {
          console.log('[Vue Tour] A custom nextStep callback has been called from step 2 to step 3')
        }
      }
    }
  }
</script>

<style scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
</style>
