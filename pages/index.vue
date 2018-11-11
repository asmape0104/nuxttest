<template>
  <section>
    定義した変数の表示<br>
    {{ data1 }}<br>
    <input type="text" v-model="data1"><br>
    v-model：変数とinputのvalueを結びつける(双方向バインディング。)<br>
    ここを編集したら変数の値は変わるし、変数の値を変えたらこっちも変わる。<br>
    なお、一個上の単なる表示部分も自動的に変化することに注目。<br>
  </section>
</template>

<script>

export default {
  // head内の情報。仕様上headの戻り値として定義。
  head() {
    return {
      title: "nuxtテスト" // <title>
    }
  },
  // 変数の定義、オブジェクトで指定する。仕様上dataの戻り値として定義。
  data() {
    return {
      data1: ""
    }
  }
}
</script>