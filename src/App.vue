<template>
  <div id="app">
    <table>
        <tr>
          <th>Név</th>
          <th>Ár</th>
          <th>Darab</th>
          <th>Operations</th>
        </tr>
        <tr :key="row.title" v-for="row in rows">

          <td v-show="!row.editing">{{row.title}}</td>
          <td v-show="!row.editing">{{row.price}}</td>
          <td v-show="!row.editing">{{row.quantity}}</td>

          <td v-show="row.editing">
            <form id="editForm"><input type="text" v-model="updTitle" name="titleIn"></form>
            </td>
          <td v-show="row.editing">
            <input form="editForm" type="number" v-model="updPrice" name="priceIn">
            </td>
          <td v-show="row.editing">
            <input form="editForm" type="number" v-model="updQuantity" name="quanIn">
            </td>

          <td>
            <button @click="toggleEdit(row)">{{ row.btnText }}</button>
            <button @click="deleteRow(row)">X</button>
          </td>

        </tr>
        <tr>
          <td colspan="4">
            <form @submit="onSubmit" id="formIn">
              <input type="text" v-model="newTitle" name="titleIn">
              <input type="number" v-model="newPrice" name="priceIn">
              <input type="number" v-model="newQuantity" name="quanIn">
              <input type="submit" value="Hozzádás">
            </form>
          </td>
        </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      rows: [
        {
          title: 'Kerék',
          price: 100,
          quantity: 12,
          editing: false,
          btnText: "Edit"
        },
        {
          title: 'Teleszkóp',
          price: 1000,
          quantity: 300,
          editing: false,
          btnText: "Edit"
        },
        {
          title: 'Kormány',
          price: 230,
          quantity: 5,
          editing: false,
          btnText: "Edit"
        },
        {
          title: 'Ajtó',
          price: 45120,
          quantity: 321,
          editing: false,
          btnText: "Edit"
        },
      ],
      newTitle: '',
      newPrice: 0,
      newQuantity: 0,
      updTitle: '',
      updPrice: 0,
      updQuantity: 0,
    }
  },
  methods: {
    deleteRow(selected) {
      this.rows = this.rows.filter((row) => row.title != selected.title)
    },
    toggleEdit(selected) {
      if(selected.editing == false) {
        selected.editing = !selected.editing
        selected.btnText = "Save"
      } else {
        this.update(selected)
        selected.editing = !selected.editing
        selected.btnText = "Edit"
      }
      
    },
    update(selected) {
      selected.title = this.updTitle
      selected.price = this.updPrice
      selected.quantity = this.updQuantity
    },
    onSubmit(e) {
      e.preventDefault()

      const newRow = {
          title: this.newTitle,
          price: this.newPrice,
          quantity: this.newQuantity,
          editing: false
      }

      this.rows = [...this.rows, newRow]

      this.title = '',
      this.price = 0,
      this.quantity = 0
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
