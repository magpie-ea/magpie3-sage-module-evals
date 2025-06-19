<!-- ParallelRatingScreen.vue -->
<template>
  <Screen :progress="progress">
    <Slide :title="'Example trial'">
      <Record
        :data="{
          trialNr: index + 1,
          itemOrder: itemOrder.join(','),
        }"
      />
      <h1>Example trial</h1>
      <span>
        Imagine the following situation:
        <br/>
        John killed the sheriff in an unusual way, by accidentally spilling poison into the sheriff's coffee.
        <br/>
        <br/>
        How natural do you find each of the following sentences for telling a friend about the situation?
        <br />
        <br />
      </span>

      <span><b>"John killed the sherrif."</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="20"
        :response.sync=$magpie.measurements[itemOrder[0]]
      />
      

      <span><b>"John accidentally poisoned the sheriff's coffee and killed him — it was a bizarre accident."</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="67"
        :response.sync=$magpie.measurements[itemOrder[1]]
      />
     

      <span><b>"John ended up killing the sheriff in a really odd way."</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="82"
        :response.sync=$magpie.measurements[itemOrder[2]]
      />
      

      <span><b>"John caused the sherrif to die."</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="78"
        :response.sync=$magpie.measurements[itemOrder[3]]
      />
      <span><b>"John shot the sheriff."</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="1"
        :response.sync=$magpie.measurements[itemOrder[4]]
      />
      
      Feel free to move the sliders to see how they work. Please press the button below once you are ready to proceed to the main experiment.
      <button
        @click="$magpie.saveAndNextScreen()"
      >
        Submit
      </button>
    </Slide>
  </Screen>
</template>

<script>


export default {
  name: 'ParallelRatingScreenExample',
  data(){
    return {response: 0}
  },
  props: {
        index: {
            type: Number,
            required: true
        },
        trial_type: {
          type: String,
          default: 'example'
        },
        progress: {
          type: Number,
          default: undefined
        },
        itemOrder: {
            type: Array,
            required: true
        },
  },
};
</script>