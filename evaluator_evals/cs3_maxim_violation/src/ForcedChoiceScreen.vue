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
          assumption: trial.assumption_name,
          correct_answer: correct_answer
        }"
      />

      
      <span v-html="createContext(trial, trial_type)">
      </span>
      <br />
      <br />
      <ForcedChoiceInput
            :response.sync= "$magpie.measurements.violation"
            :options="['Yes', 'No']" 
            @update:response="$magpie.saveAndNextScreen();"/>
      
      
    </Slide>
  </Screen>
</template>

<script>

function createContext(trial, trial_type) {
  if (trial_type == "main") {
    // if the assumption is capitalized, replace the first word with 'the speaker'
    if (trial["assumption"].charAt(0) === trial["assumption"].charAt(0).toUpperCase()) {
      var assumption = "the speaker " + _.slice(trial["assumption"].split(" "), 1).join(" ");
    } else {
      var assumption = trial["assumption"];
    }
    var context = ["In a normal conversation, you would make the following assumption about the speaker's utterance: <br /><b>", assumption, "</b>.<br/><br/>"].join("");
  } else {
    var context = [trial["assumption"], "<br />"].join("");
  }
    var question = "Do you think that the assumption is violated in this context? <br/ >" 
    var slide_text = [context, "Now imagine the following situation: ", " <br/>", trial['context'], "<br/><b> '", trial['trigger'], "'</b><br/><br/>", question].join("");
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
  name: 'ForcedChoiceScreen',
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
        correct_answer: {
          type: String,
          required: true
        },
  },
  methods: {
    createAnswerOption,
    createContext
  }
};
</script>