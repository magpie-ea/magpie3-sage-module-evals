<!-- ParallelRatingScreen.vue -->
<template>
    <Screen :progress="progress">
      <Slide>
        
        <h1>Additional Information</h1>
        <span>
        Answering the following question is optional, but it will help us analyze our results.
        </span>
        <br/>
        <div style="text-align: left; width: 350px; margin: 0 auto">
          <label
            >Age
            <input
              v-model="$magpie.measurements.age"
              type="number"
              max="110"
              min="18"
          />
        </label>
        <br/>
          <label
            >Gender
            <DropdownInput
              :options="[
                '',
                $t('screens.PostTestScreen.male'),
                $t('screens.PostTestScreen.female'),
                $t('screens.PostTestScreen.otherGender')
              ]"
              :response.sync="$magpie.measurements.gender"
            />
          </label>
          <label
            >Levels of Education
            <DropdownInput
              :options="[
                '',
                $t('screens.PostTestScreen.educationBelowHighschool'),
                $t('screens.PostTestScreen.educationHighschool'),
                $t('screens.PostTestScreen.educationCollege'),
                $t('screens.PostTestScreen.educationHigher')
              ]"
              :response.sync="$magpie.measurements.education"
            />
          </label>
          <label
            >Native languages
            <input
              v-model="$magpie.measurements.languages"
              type="text"
              :placeholder="
                $t('screens.PostTestScreen.nativeLanguagesExplanation')
              "
              :title="$t('screens.PostTestScreen.nativeLanguagesExplanation')"
          /></label>

        
        <p>Further comments</p>
        <TextareaInput
            :response.sync= "$magpie.measurements.comments"
        />
        <p>Do you think you could identify the machine-generated interpretations? If yes, how?</p>
        <TextareaInput
            :response.sync= "$magpie.measurements.llm_id"
        />
        </div>
        <button
          @click="$magpie.saveAndNextScreen()"
        >
          Next
        </button>
      </Slide>
    </Screen>
  </template>
  
  <script>
  export default {
  name: 'CustomPostTestScreen',
  data(){
    return {response: 0}
  }
};
</script>