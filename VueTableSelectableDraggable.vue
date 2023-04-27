<template>
    <div class="container mt-5">
      <div class="row">
        <h3>Vue Selectable and Draggable</h3>
      </div>
  
      <!--toggle for column customization-->
      <div>
        <b-button v-b-toggle.column-collapse variant="primary">Column</b-button>
        <b-collapse id="column-collapse" class="mt-2">
          <b-card>
            <p class="card-text">Choose the column</p>
            <b-form-checkbox-group v-model="headers">
              <b-form-checkbox value="Age">Age</b-form-checkbox>
              <b-form-checkbox value="First Name">First Name</b-form-checkbox>
              <b-form-checkbox value="Last Name">Last Name</b-form-checkbox>
            </b-form-checkbox-group>
            <b-button variant="secondary">Reset</b-button>
            <b-button variant="primary">Confirm</b-button>
          </b-card>
        </b-collapse>
      </div>
  
      <!--draggable table-->
      <div class="row">
        <table class="table table-striped">
          <thead class="thead-dark">
          <draggable v-model="headers" tag="tr" @start="onDragStart" @end="onDragEnd">
            <th v-for="header in headers" :key="header" scope="col" @mouseover="cursorChangeToMove"
                @mouseleave="cursorChangeToDefault">
              {{ header }}
            </th>
          </draggable>
          </thead>
          <tbody>
          <tr v-for="item in list" :key="item.name">
            <td v-for="header in headers" :key="header">{{ item[header] }}</td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  import draggable from 'vuedraggable';
  
  export default {
    components: {
      draggable,
    },
    data() {
      return {
        list: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { age: 38, first_name: 'Jami', last_name: 'Carney' }
        ],
        headers: ["Age", "First Name", "Last Name"],
        dragging: false,
      };
    },
    methods: {
      onDragStart() {
        this.dragging = true;
        document.body.style.cursor = 'move';
      },
      onDragEnd() {
        this.dragging = false;
        document.body.style.cursor = 'text';
      },
      cursorChangeToMove() {
        document.body.style.cursor = 'move';
      },
      cursorChangeToDefault() {
        document.body.style.cursor = 'default';
      },
    }
  }
  </script>
  
  <style>
  /* Add your styles here */
  </style>
  
