<template>
  <div id="app">

    <div style="width: 100%;">
      <div class="container-flex-tabelas">

        <h3>Tabela com createElement&amp;appendChild</h3>
        <div id="tabela-nodes" class="container-tabela">
        </div>

        <h3>Tabela com string e innerHTML</h3>
        <div id="tabela-string" class="container-tabela">
        </div>

        <h3>Tabela com uma template Vue</h3>
        <div class="container-tabela">
          <table class="tabela-exemplo">

            <tr
                v-for="(objeto, index) in arrayMock"
                :key="index"
            >

              <td
                v-for="(field, field_index) in ['nome', 'valor']"
                :key="`${index}_${field_index}`"
              >
                {{ objeto[field] }}
              </td>

            </tr>

          </table>
        </div>

        <h3>Tabela com um componente Vue</h3>
        <div class="container-tabela">
          <tabela-exemplo
            :fields="['nome', 'valor']"
            :table="arrayMock"
          />
        </div>

      </div>
    </div>

  </div>
</template>

<script>
import TabelaExemplo from './components/TabelaExemplo.vue'

export default {
  name: 'App',
  components: {
    TabelaExemplo
  },
  props: {
  },
  data () {
    return {
      arrayMock: [
        { nome: 'Sabao em Pó', valor: 10.99 },
        { nome: 'Travesseiro da Nasa', valor: 79.89 },
        { nome: 'Chinelo Azul', valor: 21.90 },
        { nome: 'Arroz 1Kg', valor: 1000.00 },
        { nome: 'Acém 1Kg', valor: 79.99 },
        { nome: 'Frango 1Kg', valor: 41.21 }
      ]
    }
  },
  methods: {
    createTable (arrayObjetos, seletor, campos) {
      if (!document.querySelector(seletor)) {
        throw Error('root selector not found')
      }

      const table = document.createElement('table')

      arrayObjetos.forEach(elemento => {
        const row = document.createElement('tr')

        campos.forEach((campo) => {
          const tableData = document.createElement('td')
          tableData.innerHTML = elemento[campo]
          row.appendChild(tableData)
        })

        table.appendChild(row)
      })

      document.querySelector(seletor).appendChild(table)
    },
    createTableString (arrayObjetos, seletor, campos) {
      if (!document.querySelector(seletor)) {
        throw Error('root selector not found')
      }

      let table = '<table>'

      arrayObjetos.forEach(elemento => {
        table += '<tr>'

        campos.forEach((campo) => {
          table += `<td> ${elemento[campo]} </td>`
        })

        table += '</tr>'
      })

      table += '</table>'
      document.querySelector(seletor).innerHTML = table
    }
  },
  mounted () {
    this.createTable(this.arrayMock, '#tabela-nodes', ['nome', 'valor'])
    this.createTableString(this.arrayMock, '#tabela-string', ['nome', 'valor'])
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
}

.container-tabela,
.container-tabela table {
  margin: 20px auto;
}

.container-tabela table {
  width: 360px;
}

.container-tabela td,
.container-tabela table {
  border: 1px solid black;
  text-align: left;
}

.container-tabela td {
  padding: 6px 4px;
}

.container-tabela table {
  padding: 4px 8px;
}

</style>
