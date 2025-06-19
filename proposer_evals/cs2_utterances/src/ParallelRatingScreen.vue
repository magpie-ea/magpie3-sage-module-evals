<!-- ParallelRatingScreen.vue -->
<template>
  <Screen :progress="progress">
    <Slide>
      <Record
        :data="{
          trialNr: index + 1,
          vignette: trial.vignette,
          trial_type: trial_type,
          state_type: trial.state_type,
          itemOrder: itemOrder.join(','),
        }"
      />

      
      <span v-html="createContext(trial)">
      </span>
      <br />
      <br />
      <span v-html="createAnswerOption(trial, itemOrder[0])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[0]]
      />
      

      <span v-html="createAnswerOption(trial, itemOrder[1])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[1]]
      />
     

      <span v-html="createAnswerOption(trial, itemOrder[2])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[2]]
      />
      

      <span v-html="createAnswerOption(trial, itemOrder[3])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[3]]
      />
      <span v-html="createAnswerOption(trial, itemOrder[4])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[4]]
      />
      
      <button
        v-if="checkResponses(
            $magpie.measurements[itemOrder[0]],
            $magpie.measurements[itemOrder[1]],
            $magpie.measurements[itemOrder[2]],
            $magpie.measurements[itemOrder[3]],
            $magpie.measurements[itemOrder[4]],
        )"
        @click="$magpie.saveAndNextScreen()"
      >
        Submit
      </button>
    </Slide>
  </Screen>
</template>

<script>

function createContext(trial) {
    var slide_text = ["Imagine the following situation: ", " <br/><b>", trial['state'], "</b><br/>", "How natural do you find each of the following sentences for telling a friend about the situation?"].join("");
    return slide_text
}

function createAnswerOption(trial, option) {  
      
      var slide_text = ['<b>"', trial[option], '"</b>'].join("");
      
      
      //if (option != "itemQuestion") {
      //  var slide_text = ["<br/>","... they ", trial["priorElicitation_question"], " <b>", alternative, "</b> instead?"].join("");
      //} else {
      //  var slide_text = ["<br/>","... they ", trial["priorElicitation_question"], " <b>", alternative, "</b>?"].join("");
      //}
      
      return slide_text
}
export default {
  name: 'ParallelRatingScreen',
  data(){
    return {response: 0}
  },
  props: {
    trial: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        },
        trial_type: {
          type: String,
          required: true
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
  methods: {
    checkResponses: function (a, b, c, d, e) {
      return !(isNaN(a) | isNaN(b) | isNaN(c) | isNaN(d) | isNaN(e));
    },
    createAnswerOption,
    createContext
  }
};
</script>