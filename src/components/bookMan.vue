<template>
  <div>
    <input type="search" placeholder="搜索-书本名称" class="search">
    <table>
      <thead>
        <th>序号</th>
        <th>书名</th>
        <th>作者</th>
        <th>出版商</th>
        <th>操作</th>
      </thead>
      <tbody>
        <tr>
          <td>1</td>
          <td>1</td>
          <td>1</td>
          <td>1</td>
          <td>1</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  methods: {
  }

}
</script>

<style>
  .search{
    font-size: 15px;
    padding: 5px 0;
    padding-left: 10px;
  }
  table{
    margin-top: 10px;
    width: 800px;
    border-collapse: collapse;
    text-align: left;
  }
  th,
  td{
    border: 1px solid #ccc;
    height: 30px;
    padding-left: 5px;
  }
  thead{
    border-bottom: 2px solid black;
  }
</style>