<template>
  <div class="about">
    <h1>This is a list data</h1>
    <v-app id="table">
      <v-data-table :headers="headers" :items="listItem" :items-per-page="2" class="elevator">
        <!-- header-->
        <template #header.name="{header}"> {{ header.text.toUpperCase() }}</template>
        <template #header.age="{header}"> {{ header.text.toUpperCase() }}</template>
        <template #header.serial="{header}"> {{ header.text.toUpperCase() }}</template>
        <template #header.actions="{header}"> {{ header.text.toUpperCase() }}</template>

        <!--button edit and delete each of row data-->
        <template #item.actions="{item}">
          <v-icon small class="mr-2" color="warning" @click="handleState(item, null)">mdi-pencil</v-icon>
          <v-icon small class="mr-2" color="error" @click="handlePopup(item)">mdi-delete</v-icon>
        </template>

      </v-data-table>
      <v-dialog v-model="modalDialog" width="500px">
        <template #activator="{on, attrs}">
          <v-btn
              dark
              color="primary"
              class="btn-add"
              @click="handleState()"
              v-bind="attrs"
              v-on="on"
          >
            new item
          </v-btn>
        </template>
        <!--...-->
        <v-card>
          <!--title-->
          <v-card-title class="black lighten-2">Add new here</v-card-title>
          <!--title-->
          <!--inputs-->
          <div id="field">
            <v-text-field
                label="name"
                placeholder="Placeholder"
                outlined class="text-field"
                @change="(name) => setState(name, 'name')"
                :value="dataObj.name"
            >
            </v-text-field>
            <v-text-field
                label="age"
                placeholder="Placeholder"
                outlined
                class="text-field"
                @change="(age) => setState(age, 'age')"
                :value="dataObj.age"
            >
            </v-text-field>
            <v-text-field
                label="serial-number"
                placeholder="Placeholder"
                outlined class="text-field"
                @change="(serial) => setState(serial, 'serial')"
                :value="dataObj.serial"
            >
            </v-text-field>
          </div>
          <!--input-->
          <v-divider></v-divider>
          <!--actions-->
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn text color="teal" class="ma-2" dark outlined @click="handleFunc(dataObj.id)">
              <v-icon dark left>mdi-checkbox-marked-circle</v-icon>
              {{ statusAction }}
            </v-btn>
            <v-btn text color="secondary" class="ma-2" dark outlined @click="handleState()">
              <v-icon dark left>mdi-cancel</v-icon>
              cancel
            </v-btn>
          </v-card-actions>
          <!--actions-->
        </v-card>
      </v-dialog>
      <!--Popup-->
      <v-dialog v-model="modalPopup" width="500px">
        <v-card>
          <v-card-title class="black lighten-2">Are you sure to remove {{ nameRemove }}</v-card-title>
        </v-card>
        <div class="modal-popup">
          <v-btn color="error">
            <v-icon small class="mr-2" color="white">mdi-delete</v-icon>
            Delete
          </v-btn>
          <v-btn class="grey" @click="handlePopup">
            <v-icon dark left>mdi-cancel</v-icon>
            Cancel
          </v-btn>
        </div>
      </v-dialog>
    </v-app>
  </div>
</template>

<script>

export default {
  data: () => {
    return {
      headers: [
        {text: "name", value: 'name'},
        {text: "age", value: 'age'},
        {text: "serial", value: 'serial'},
        {text: "action", value: 'actions'}
      ],
      listItem: [
        {
          id: 1,
          name: "ABC",
          age: 23,
          serial: "@#SSXXXXXXXXXXXX"
        },
        {
          id: 2,
          name: "ZYZ",
          age: 45,
          serial: "XXXXSWEWFSGBBBBB"
        },
        {
          id: 3,
          name: "LSS",
          age: 24,
          serial: "SDWDWDSDSSDSDSDS"
        },
      ],
      modalDialog: false,
      modalPopup: false,
      dataObj: {
        id: null,
        name: '',
        age: '',
        serial: ''
      },
      statusAction: 'save',
      nameRemove: ''
    }
  },
  methods: {
    handlePopup: function(data){
      this.modalPopup = !this.modalPopup;
      this.nameRemove = data.name;
    },
    handleState: function (data, keyObj) {
      //open or close modal
      this.modalDialog = !this.modalDialog;
      //Case add new item
      if (!data) {
        this.statusAction = 'save'
        return this.resetState();
      }
      //Case update, delete
      return this.setState(data, keyObj);
    },
    setState: function (data, keyObj) {
      let {id, name, serial, age} = data;
      switch (keyObj) {
        case null:
          this.dataObj = Object.assign({id, name, age, serial})
          this.statusAction = 'update'
          return;
        default:
          this.dataObj[keyObj] = data;
          return;
      }
    },
    resetState: function () {
      this.dataObj = {id: null, name: '', age: '', serial: ''}
    },
    handleFunc: function () {
      switch (this.statusAction) {
        case "update":
          console.log(`Data là:`, {...this.dataObj})
          break;
        case "save":
          console.log(`Data là: `, {name: this.dataObj.name, age: this.dataObj.age, serial: this.dataObj.serial})
      }
    }
  }
}
</script>

<style>
#table {
  width: 60%;
  margin: auto;
}

.btn-add {
  width: 15%;
  margin-left: auto;
}

.text-field {
  width: 50%;
  margin: auto !important;
}

#field {
  margin-top: 30px
}

.v-card__title {
  color: white
}
.modal-popup{
  height: 100px;
  background: white;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
</style>
