<template>
  <table class="tabela-exemplo">

    <tr
        v-for="(objeto, index) in table"
        :key="index"
    >

      <td
        v-for="(field, field_index) in fields"
        :key="`${index}_${field_index}`"
      >
        {{ objeto[field] }}
      </td>

    </tr>

  </table>
</template>

<script>
export default {
  name: 'TabelaExemplo',
  props: {
    msg: String,
    fields: Array,
    table: Array,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
