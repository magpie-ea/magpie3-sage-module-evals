<template>
  <Experiment title="magpie demo">
    <InstructionScreen :title="'Welcome'">
      Thanks for taking part in our experiment! The experiment will take approximately 2-3 minutes.
      <br />
      <br />
      In this experiment, we will ask you what you think about other people's intentions in everyday contexts.
      On each trial, you will read a short description of a situation wherein a person utters a sentence. 
      <b>We will ask you if you think a statement about that person's uttance is true or false.</b> Please try to respond naturally and reasonably.
      <br />
      <br />
      Notice that there will also be a simple <b>attention checking trial</b>. 
      You will recognize it immediately when you read the important text on each trial carefully -- this trial contains instructions for you to answer in a certain way.
      Please follow these instructions on the respective trial. 
      <br />
      <br />
      You are participating in a study conducted by cognitive scientists at the University of Tübingen. 
      Your participation in this research is voluntary.
      You may decline to answer any or all of the following questions.
      You may decline further participation, at any time, without adverse consequences.
      <br />
      <br />
      Your anonymity is assured; the researchers who have requested your
      participation will not receive any personal information about you.
      <br />
      <br />
      By pressing the button 'Next' you confirm that you are at least 18 years old and agree to participate in this study. You will then start the main experiment. 
    </InstructionScreen>

    <template v-for="(trial, i) in trials"> 
      <template v-if="Object.keys(trial).includes('correct_answer')">      
        <ForcedChoiceScreen 
            :trial=trial
            :index=i 
            :trial_type="'filler'" 
            :progress="i / trials.length" 
            :correct_answer="trial.correct_answer"
        />   
      </template>
      <template v-else>
        <ForcedChoiceScreen 
            :trial=trial
            :index=i 
            :trial_type="'main'" 
            :progress="i / trials.length" 
            :correct_answer="'main'"
        />   
      </template>   
    </template>

    <PostTestScreen />
    <SubmitResultsScreen />
  </Experiment>
</template>

<script>
import _ from 'lodash';
import trialsAll from '../trials/trials.csv';
import ForcedChoiceScreen from './ForcedChoiceScreen';
import fillers from '../trials/fillers.csv';

var condition = ['too_much', 'too_little', 'marked', 'irrelevant', 'baseline'];
var maxims = _.sampleSize(['quantity_1', 'quantity_2', 'quality_1', 'quality_2', 'relevance_1', 'manner_1', 'manner_2', 'manner_3', 'manner_4'], 5);

var n_fillers = 1;

function filterByCondition(data) {
  const conditionMap = {}
  condition.forEach((item, i) => {
    conditionMap[item] = maxims[i]
  })

  return data.filter(row => {
    return conditionMap[row.inference_type] === row.assumption_name
  })
}

const sampled_trials = filterByCondition(trialsAll);
// Disable selecting text
// Supported by the following browsers:
// https://caniuse.com/mdn-api_document_selectstart_event
document.onselectstart = () => false;

// Disable context menu
// Supported by the following browsers:
// https://caniuse.com/mdn-api_element_contextmenu_event
document.oncontextmenu = () => false;

export default {
  name: 'App',
  components: { 
    ForcedChoiceScreen
  },
  data() {
    return {
      trials: _.shuffle(_.concat( sampled_trials, _.sampleSize(fillers, n_fillers))) //
    };
  },
  computed: {
    // Expose lodash to template code
    _() {
      return _;
    }
  }
};
</script>
