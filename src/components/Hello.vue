<template>
  <div class="fluid">
<!-- fluid container
On hold | Proposal | Discovery | Design | Delivery | QA | Suuport
-->
      <div>
        <draggable element="span" v-model="listPending" :options="dragOptions" :move="onMove" class="list-group" @end="onEnd"> 
            <transition-group name="no" class="list-group" tag="ul">
              <li class="list-group-item" v-for="element in listPending" :key="element.order"> 
                <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                {{element.name}}
              </li> 
            </transition-group>
        </draggable>
      </div>

<table class="table">
  <thead>
    <tr>
      <th v-for="column in columns" >{{column}}</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="card in cards">
      <th scope="row">{{card.name}}</th>
      <td class="col-sm-2">
        <div>
          <draggable element="span" v-model="list" :options="dragOptions" :move="onMove" class="list-group"> 
              <transition-group name="no" class="list-group" tag="ul">
                <li class="list-group-item" v-for="element in card.personalCards.onhold" :key="element.order"> 
                  <i :class="element.fixed? 'fa fa-pencil' : 'fa fa-pencil'" @click="test" aria-hidden="true"></i>
                  {{element.name}}
                </li> 
              </transition-group>
          </draggable>
        </div>
      </td>

      <td class="col-sm-2">
        <div>
          <draggable element="span" v-model="list" :options="dragOptions" :move="onMove" class="list-group"> 
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
          <draggable element="span" v-model="list" :options="dragOptions" :move="onMove" class="list-group"> 
              <transition-group name="no" class="list-group" tag="ul">
                <li class="list-group-item" v-for="element in card.personalCards.discovery" :key="element.order"> 
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
const message = ["draggable", "component", "for"];
const listPending1 = ["draggable1", "component1", "for1"];

export default {
  name: "hello",
  components: {
    draggable
  },
  data() {
    return {
      // members: ['Piers', 'Stefan', 'Martin', 'Dean'],
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
      cards: [
        {
          name: "Piers",
          personalCards: {
            onhold: [
              {
                name: "Card 1",
                order: 1,
                fixed: false
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
            ]
          }
        },
        {
          name: "Stefan",
          personalCards: []
        },
        {
          name: "Dean",
          personalCards: []
        }
      ],
      list: message.map((name, index) => {
        return { name, order: index + 1, fixed: false };
      }),
      listPending: listPending1.map((name, index) => {
        return { name, order: index + 1, fixed: false };
      }),
      list2: [],
      list3: [],
      list4: [],
      list5: [
        {
          name: "",
          order: 1000,
          fixed: false,
          visible: false
        }
      ],
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
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      // console.log(relatedElement)
      return (
        (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      );
    },
    onEnd(evt, originalEvent) {
      console.log(evt, originalEvent);
    },
    test() {
      console.log("test");
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
    },
    listString() {
      console.log(JSON.stringify(this.list, null, 2));
      return JSON.stringify(this.list, null, 2);
    },
    list2String() {
      return JSON.stringify(this.list2, null, 2);
    },
    list3String() {
      return JSON.stringify(this.list3, null, 2);
    },
    list4String() {
      return JSON.stringify(this.list4, null, 2);
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
  background-color: lightgray;
}

.list-group-item {
  cursor: move;
}

.list-group-item i {
  cursor: pointer;
}
</style>

