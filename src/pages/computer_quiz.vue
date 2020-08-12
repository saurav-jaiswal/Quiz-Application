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
              <q-item-label>Computer Quiz</q-item-label>
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
                        question: 'Which mouse click is used to select item?',
                        suggestions: [
                            {suggestion: 'Single click', correct: true},
                            {suggestion: 'Double click'},
                            {suggestion: 'Right click'},
                            {suggestion: 'Drag and drop'}
                        ]
                    },
                    {
                        question: 'Which key allows to cancel an operation?',
                        suggestions: [
                            {suggestion: 'Shift key'},
                            {suggestion: 'Escape key', correct: true},
                            {suggestion: 'Enter key'},
                            {suggestion: 'Space bar key'},

                        ]
                    },
                    {
                        question: 'These keys have special signs and symbols on them.',
                        suggestions: [
                            {suggestion: 'Number keys'},
                            {suggestion: 'Letter keys'},
                            {suggestion: 'Symbol keys', correct: true},
                            {suggestion: 'Function keys'},
                        ]
                    },
                    {
                        question: 'This key is used with other keys for different purposes.',
                        suggestions: [

                            {suggestion: 'Enter key'},
                            {suggestion: 'Backspace key'},
                            {suggestion: 'Tab key'},
                            {suggestion: 'Shift key', correct: true}

                        ]
                    },{
                        question: 'The first mechanical computer designed by Charles Babbage was called ?',
                        suggestions: [

                            {suggestion: 'Abacus'},
                            {suggestion: 'Calculator'},
                            {suggestion: 'Analytical Engine', correct: true},
                            {suggestion: 'Processor'}

                        ]
                    },{
                        question: ' Which is a single integrated circuit?',
                        suggestions: [

                            {suggestion: 'Gate', correct: true},
                            {suggestion: 'Chip'},
                            {suggestion: 'Mother Board'},
                            {suggestion: 'CPU'}

                        ]
                    },{
                        question: 'Which of the following is an example of non volatile memory ?',
                        suggestions: [

                            {suggestion: 'VLSI'},
                            {suggestion: 'LSI'},
                            {suggestion: 'ROM', correct: true},
                            {suggestion: 'RAM'}

                        ]
                    },{
                        question: 'Graphic interfaces were first used in a xerox product is called ?',
                        suggestions: [

                            {suggestion: 'Ethernet', correct: true},
                            {suggestion: 'Inter LISP'},
                            {suggestion: 'Small talk'},
                            {suggestion: 'Zeta LISP'}

                        ]
                    },{
                        question: 'The first movie released in 1982 with terrific computer animation and graphics was ?',
                        suggestions: [

                            {suggestion: 'Star wars', correct: true},
                            {suggestion: 'Tron'},
                            {suggestion: ' Forbidden planet'},
                            {suggestion: 'Dark star'}

                        ]
                    },{
                        question: 'The parity bit is added for the purpose of ?',
                        suggestions: [

                            {suggestion: 'Coding'},
                            {suggestion: 'Controlling'},
                            {suggestion: 'Error detection', correct: true},
                            {suggestion: 'Indexing'}

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

            },
            //  initNamesArray() {
            //     this.questions = this.shuffle(this.questions)
            //     console.log('this.questions:', this.questions)
            // },
            // shuffle(a) {
            //     var j, x, i;
            //     for (i = a.length - 1; i > 0; i--) {
            //         j = Math.floor(Math.random() * (i + 1));
            //         x = a[i];
            //         a[i] = a[j];
            //         a[j] = x;
            //     }
            //     return a;
            // },

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
