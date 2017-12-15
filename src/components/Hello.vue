<template>
  <div class="fluid">
    <div>
      <draggable element="span" v-model="cards.pending" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
          <transition-group name="no" class="list-group" tag="ul">
            <li class="list-group-item" v-for="element in cards.pending" :key="element.order"> 
              <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
              {{element.name}}
            </li> 
          </transition-group>
      </draggable>
    </div>

<!-- <li class="list-group-item" v-for="element in card.personalCards.onhold" :key="element.order"> 
  <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
  {{element.name}}
</li>  -->

    <table class="table">
      <thead>
        <tr>
          <th v-for="column in columns" >{{column}}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="card in cards.assigned">
          <th scope="row">{{card.name}}</th>
          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.onhold" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <card  v-for="element in card.personalCards.onhold" v-bind:key="element.order" :element="element"></card>
                  </transition-group>
              </draggable>
            </div>
          </td>

          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.proposal" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in card.personalCards.proposal" :key="element.order"> 
                      <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                      {{element.name}}
                    </li> 
                  </transition-group>
              </draggable>
            </div>
          </td>

          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.discovery" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in card.personalCards.discovery" :key="element.order"> 
                      <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                      {{element.name}}
                    </li> 
                  </transition-group>
              </draggable>
            </div>
          </td>  

          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.design" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in card.personalCards.design" :key="element.order"> 
                      <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                      {{element.name}}
                    </li> 
                  </transition-group>
              </draggable>
            </div>
          </td>   

          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.delivery" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in card.personalCards.delivery" :key="element.order"> 
                      <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                      {{element.name}}
                    </li> 
                  </transition-group>
              </draggable>
            </div>
          </td>  

          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.qa" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in card.personalCards.qa" :key="element.order"> 
                      <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                      {{element.name}}
                    </li> 
                  </transition-group>
              </draggable>
            </div>
          </td>  

          <td class="col-sm-2">
            <div>
              <draggable element="span" v-model="card.personalCards.support" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
                  <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in card.personalCards.support" :key="element.order"> 
                      <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                      {{element.name}}
                    </li> 
                  </transition-group>
              </draggable>
            </div>
          </td>                                              

        </tr>
      </tbody>
    </table>
<!-- <pre>{{listString}}</pre> -->
  </div>
</template>

<script>
import draggable from "vuedraggable";
import card from "./Card";

export default {
  name: "hello",
  components: {
    draggable, card
  },
  data() {
    return {
      columns: [
        "Member",
        "On hold",
        "Proposal",
        "Discovery",
        "Design",
        "Delivery",
        "QA",
        "Support"
      ],
      cards: {
        pending: [
          {
            name: "Card 101",
            order: 1,
            fixed: false,
            details: "123"
          },
          {
            name: "Card 102",
            order: 2,
            fixed: false
          },
          {
            name: "Card 103",
            order: 3,
            fixed: false
          }
        ],
        assigned: [
          {
            name: "Piers",
            personalCards: {
              onhold: [
                {
                  name: "Card 1",
                  order: 1,
                  fixed: false,
                  details: "123"
                },
                {
                  name: "Card 2",
                  order: 2,
                  fixed: false
                },
                {
                  name: "Card 3",
                  order: 3,
                  fixed: false
                }
              ],
              proposal: [],
              discovery: [
                {
                  name: "Card 4",
                  order: 1,
                  fixed: false
                },
                {
                  name: "Card 5",
                  order: 2,
                  fixed: false
                },
                {
                  name: "Card 6",
                  order: 3,
                  fixed: false
                }
              ],
              design: [],
              delivery: [],
              qa: [],
              support: []
            }
          },
          {
            name: "Stefan",
            personalCards: {
              onhold: [],
              proposal: [],
              discovery: [],
              design: [],
              delivery: [],
              qa: [],
              support: []
              
            }
          },
          {
            name: "Dean",
            personalCards: {
              onhold: [],
              proposal: [],
              discovery: [],
              design: [],
              delivery: [],
              qa: [],
              support: []
            }
          }
        ]
      },
      list: {},
      editable: true,
      isDragging: true,
      delayedDragging: true
    };
  },
  methods: {
    orderList() {
      this.list = this.list.sort((one, two) => {
        return one.order - two.order;
      });
    },
    onMove({ relatedContext, draggedContext }) {
      // console.log(relatedContext);
      // console.log(draggedContext);
      // console.log("test");
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;

      return (
        (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      );
    },
    onEnd(evt, originalEvent) {
      // console.log("test123");
      //console.log(evt, originalEvent);
    },
    test(evt) {
      console.log(this);
    }
  },
  computed: {
    dragOptions() {
      return {
        animation: 0,
        group: "description",
        disabled: !this.editable,
        ghostClass: "ghost"
      };
    }
  },
  watch: {
    isDragging(newValue) {
      if (newValue) {
        this.delayedDragging = true;
        return;
      }
      this.$nextTick(() => {
        this.delayedDragging = false;
      });
    }
  }
};
</script>

<style>
.table > tr > td {
  vertical-align: top !important;
}
.flip-list-move {
  transition: transform 0.5s;
}

.no-move {
  transition: transform 0s;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.hidden {
  /* display: block */
}

.list-group {
  min-height: 42px;
  background-color: #efefef;
}

.list-group-item {
  cursor: move;
}

.list-group-item i {
  cursor: pointer;
}
</style>

