<template>
  <q-page padding>
    <div class="row">
      <div class="col">
        <q-card class="my-card">
          <q-item>
            <q-item-section avatar>
              <q-avatar>
               <q-icon name="account_circle" size="lg" style="color: #333847"></q-icon>
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label>Current Affairs Quiz</q-item-label>
              <q-item-label caption>Play Quiz Online</q-item-label>
            </q-item-section>
          </q-item>

          <q-card-section class="">
            <h4 class="text-center">Questions {{b}}/ {{questions.length}}</h4>
            <div v-for="(element,index) in questions.slice(a,b)" :key="index" class="text-center" v-show="quiz_modal">
              <h5>
                {{element.question}}
              </h5>
              <div>
                <ul>
                  <q-btn class="q-ma-sm" :class="select ? check(item) : ''" v-for="item in element.suggestions"
                         @click="selectResponse(item)">{{item.suggestion}} &nbsp
                    <div class="fas fa-check" v-if="select ? item.correct :''"></div>
                    &nbsp
                    <div class="fas fa-times" v-if="select ? !item.correct :''"></div>
                  </q-btn>
                </ul>
              </div>

            </div>
            <div v-if="score_show_modal" class="text-center">
              <h3>Your Score is</h3>
              <h4>{{score}}/{{questions.length}}</h4>
            </div>
          </q-card-section>

          <q-separator/>

          <q-card-actions align="right" v-if="quiz_modal">
            <q-btn :style="!next ? 'background-color:rgb(106,128,202)' :''" @click="skipQuestions">Skip</q-btn>
            <q-btn :style="next ? 'background-color:rgb(106,128,202)' :''" @click="nextQuestions">Next</q-btn>
          </q-card-actions>
           <q-card-actions align="right" v-if="!quiz_modal">
            <q-btn :style="next ? 'background-color:rgb(106,128,202)' :''" to="/">Home</q-btn>
          </q-card-actions>

        </q-card>
      </div>
    </div>

  </q-page>
</template>

<script>
    export default {
        name: "quiz1",
        data() {
            return {
                step: 0,
                progress: 0,
                questions: [
                    {
                        question: 'Which Ministry launched the Portal Surakhsya?',
                        suggestions: [
                            {suggestion: 'Ministry of Environment, Forest and Climate Change', correct: true},
                            {suggestion: 'Ministry of New and Renewable Energy'},
                            {suggestion: 'Ministry of Electronics and Information '},
                            {suggestion: 'Ministry of Health and Family Welfare'}
                        ]
                    },
                    {
                        question: 'Who is the founder of Vanya Organic?',
                        suggestions: [
                            {suggestion: 'Ritu Karidhal'},
                            {suggestion: 'Shanti Swaroop'},
                            {suggestion: 'Aditi Pant'},
                            {suggestion: 'Patanjali', correct: true},

                        ]
                    },
                    {
                        question: 'Who assumed charge as the Principal Chief Commissioner of Income Tax, Mumbai?',
                        suggestions: [
                            {suggestion: 'Rajnish D. Burman'},
                            {suggestion: 'Patanjali', correct: true},
                            {suggestion: 'Sanjay Puri'},
                            {suggestion: 'S.B. Singh'},
                        ]
                    },
                    {
                        question: 'What is the theme for the 2020 World Biofuel day?',
                        suggestions: [

                            {suggestion: 'Way of Escape and milestone to Achieve Atmanirbhar Bharat'},
                            {suggestion: 'Atmanirbhar Bharat - Sustainable Biofuels'},
                            {suggestion: 'Biofuels towards Atmanirbhar Bharat', correct: true},
                            {suggestion: 'None'}

                        ]
                    },
                    {
                        question: 'When was the submarine Optical Fibre Cable (OFC) Project laid by Prime Minister Narendra Modi?',
                        suggestions: [

                            {suggestion: '2016'},
                            {suggestion: '2017'},
                            {suggestion: '2018', correct: true},
                            {suggestion: '2019'}

                        ]
                    },
                    {
                        question: 'When is the World Biofuel day observed?',
                        suggestions: [

                            {suggestion: '2 August'},
                            {suggestion: '5 August'},
                            {suggestion: '7 August'},
                            {suggestion: '10 August', correct: true}

                        ]
                    },
                    {
                        question: 'Who is appointed as the Chairman of UPSC?',
                        suggestions: [

                            {suggestion: 'Shri Arvind Saxena'},
                            {suggestion: 'Prof. Dr. Pradeep Kumar Joshi', correct: true},
                            {suggestion: 'Dr. A. S. Bhonsle'},
                            {suggestion: 'Ms. Sujata Mehta'}

                        ]
                    },
                    {
                        question: 'When was the International Day of the World\'s Indigenous Peoples observed?',
                        suggestions: [

                            {suggestion: '30 July'},
                            {suggestion: '9 August', correct: true},
                            {suggestion: '15 August'},
                            {suggestion: '30 August'}

                        ]
                    },
                    {
                        question: 'When was TRIFED established?',
                        suggestions: [

                            {suggestion: '1975'},
                            {suggestion: '1982'},
                            {suggestion: '1980'},
                            {suggestion: '1987', correct: true}

                        ]
                    },
                    {
                        question: 'When is the Quit India Day observed?',
                        suggestions: [

                            {suggestion: '1 August'},
                            {suggestion: '9 August', correct: true},
                            {suggestion: '5 August'},
                            {suggestion: '12 August'}

                        ]
                    },
                ],

                a: 0,
                b: 1,
                select: false,
                score: 0,
                quiz_modal: true,
                score_show_modal: false,
                next: false,
            }
        },
        methods: {
            selectResponse(e) {
                this.select = true;
                this.next = true;
                if (e.correct) {
                    this.score++
                }
            },
            check(status) {
                if (status.correct) {
                    return 'correct'
                } else {
                    return 'incorrect'
                }
            },
            nextQuestions() {
                if (!this.next) {
                    return;
                }

                if (this.questions.length - 1 == this.a) {
                    this.score_show_modal = true;
                    this.quiz_modal = false
                } else {
                    this.a++;
                    this.b++;
                    this.select = false;
                    this.next = false;
                }

            },
            skipQuestions() {
                if (this.next) {
                    return;
                }

                if (this.questions.length - 1 == this.a) {
                    this.score_show_modal = true;
                    this.quiz_modal = false
                } else {
                    this.a++;
                    this.b++;
                    this.select = false
                }

            }

        }
    }
</script>

<style scoped>
  .q-btn{
    background-color: rgb(51,56,71);
    color: white;
     border: 1px solid rgb(105, 105, 105);

  }
  .q-btn.correct {
    border: 1px solid rgb(74, 219, 74);
    background-color: rgb(31, 153, 31);
    color: white;
    font-weight: 600;
  }

  .q-btn.incorrect {
    border: 1px solid rgb(240, 117, 100);
    background-color: rgb(240, 117, 100);
    color: white;
    font-weight: 600;
  }


</style>
