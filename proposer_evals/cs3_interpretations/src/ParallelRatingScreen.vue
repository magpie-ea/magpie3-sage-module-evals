<!-- ParallelRatingScreen.vue -->
<template>
  <Screen :progress="progress">
    <Slide>
      <Record
        :data="{
          trialNr: index + 1,
          item_id: trial.item_id,
          trial_type: trial_type,
          inference_type: trial.inference_type,
          assumption: trial.assumption,
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
      <br />
      <span v-html="createAnswerOption(trial, itemOrder[1])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[1]]
      />
      <br />

      <span v-html="createAnswerOption(trial, itemOrder[2])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[2]]
      />
      <br />

      <span v-html="createAnswerOption(trial, itemOrder[3])"></span>
      <SliderInput
        left="terrible"
        right="natural"
        initial="50"
        :response.sync=$magpie.measurements[itemOrder[3]]
      />
      
      <button
        v-if="checkResponses(
            $magpie.measurements[itemOrder[0]],
            $magpie.measurements[itemOrder[1]],
            $magpie.measurements[itemOrder[2]],
            $magpie.measurements[itemOrder[3]]
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
    var explanation_question = trial['explanation'] === "" ? "How natural does each of the following sentences express what the speaker could plausibly want to convey?" : ["Assuming that ", trial['explanation'], ", how natural does each of the following sentences express what the speaker could plausibly want to convey?"].join("") ;
    var slide_text = ["Imagine the following situation: ", " <br/>", trial['context'], "<br/><b> ", trial['utterance'], "</b><br/><br/>", explanation_question].join("");
    return slide_text
}

function createAnswerOption(trial, option) {  
      
      var slide_text = ["<b>",trial[option], "</b>"].join("");
      
      
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
        targetOption: {
          type: String,
          required: true
        },
  },
  methods: {
    checkResponses: function (a, b, c, d) {
      return !(isNaN(a) | isNaN(b) | isNaN(c) | isNaN(d) );
    },
    createAnswerOption,
    createContext
  }
};
</script>