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
        Alex made cookies for Bam and Bam tried them. You ask Bam: "How are Alex' cookies?" Bam replies: "They tasted healthy."  
        <br/>
        <br/>
        Assuming that the answer is intentionally ambiguous in the context, how natural does each of the following sentences express what the speaker could plausibly want to convey?
        <br />
        <br />
      </span>

      <span><b>Bam might be trying to convey that the cookies were healthy.</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="20"
        :response.sync=$magpie.measurements[itemOrder[0]]
      />
      

      <span><b>Bam might be implying the cookies lacked flavor, richness, or indulgence, often associated with treats, but is avoiding direct negativity by using a neutral term like "healthy.".</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="75"
        :response.sync=$magpie.measurements[itemOrder[1]]
      />
     

      <span><b>Bam might be trying to convey that the cookies were not good, but they want to be polite to Alex.</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="82"
        :response.sync=$magpie.measurements[itemOrder[2]]
      />
      

      <span><b>Bam could be suggesting the cookies were nutritious but not particularly enjoyable, hinting they were dry, bland, or overly focused on health at the expense of taste.</b></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="78"
        :response.sync=$magpie.measurements[itemOrder[3]]
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