<template>
  <section>
    定義した変数の表示<br>
    {{ data1 }}<br>
    <hr>

    <input type="text" v-model="data1"><br>
    v-model：<br>
    変数とinputのvalueを結びつける(双方向バインディング。)<br>
    ここを編集したら変数の値は変わるし、変数の値を変えたらこっちも変わる。<br>
    なお、一個上の単なる表示部分も自動的に変化することに注目。<br>
    <hr>

    <a v-bind:href="data2">リンク1</a>
    <a :href="data2">リンク2</a>
    <br>
    v-bind:属性名<br>
    value以外の属性と変数を結びつけるときに使う。v-bindを省略して「:属性名」もいける。<br>
    変数が書き換わればちゃんと反映される。
    <hr>

    <select v-model="data3">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <div v-if="data3 == 1">
      1が選択されています。
    </div>
    <div v-else-if="data3 == 2">
      2が選択されています。
    </div>
    <div v-else>
      １,2以外が選択されています。
    </div>
    v-if、v-else、v-else-if:<br>
    if文のようなもの。条件を満たした要素が表示されそれ以外は隠される。<br>
    v-modelでdata3がいじれるが変数が操作されたときにちゃんと表示も切り替わることに注目。
    <hr>

    <input type="checkbox" v-model="data4" value="check"> チェック
    <div v-show="data4">ヨーソロー</div>
    <br>
    v-show:<br>
    条件式が成り立ったときに表示される。v-ifとの違いは<br>
    ・v-elseなどが使えない<br>
    ・条件が成り立たなかったとき、v-ifは本当に消えるのに対してv-showはdisplay: noneするだけ<br>
    の2つ
    <hr>

    <ul>
      <li v-for="d in data5" :key="d">{{ d }}</li>
    </ul>
    <ul>
      <li v-for="(value, key) in data6" :key="key">{{ key }}: {{ value }}</li>
    </ul>
    <span v-for="i in 10" :key="i">{{ i }}</span>
    <br>
    v-for:<br>
    いわゆるループ。<br>
    ①配列や、オブジェクトのvalueのみが欲しい場合のループ(for-of)。<br>
    ②オブジェクトのkeyとvalueが欲しい場合のループ。<br>
    ③1から指定した数まで繰り返すループ(普通のfor)<br>
    の3つの書き方がある。<br>
    v-forを設定した要素を繰り返し表示する。<br>
    (v-bind):key属性に要素を区別するためのデータを指定しなければならない。通常はループで取り出したデータでよい。<br>
    数値のループは1からなので注意。
    <hr>
    <button v-on:click="button1">ボタン1</button>
    <button @click="button1">ボタン2</button><br>
    v-on:イベント名<br>
    イベントを設定する。「v-on:」を「@」にしてもいける。
    <hr>
    <input type="checkbox" v-model="data7" value="check"> チェック
    <template v-if="data7">
      <div>ヨーソロー</div>
      <div>みかん</div>
    </template>
    template要素:<br>
    v-if、v-else-if、v-else、v-forは、指定した要素に適用されるという性質上、一つの要素にしか適用できない。<br>
    つまり、条件を満たしたら2つの要素を表示するといったことがそのままではできない。<br>
    これを解決するのがtemplate要素である。<br>
    template要素は実際に要素としては描画されない。<br>
    何を言っているかわからんと思ったらブラウザの検証で構造を見てみるといいと思う。
    <hr>
    <radio name="a" value="radio1">69webの使い回し</radio><br>
    <radio name="a" value="radio2">69webの使い回し</radio><br>
    コンポーネント<br>
    vueではタグを作れる。<br>
    これをコンポーネントと呼ぶ。<br>
    詳しくはcomponents/timetable_radio.vueも参照。
    <hr>
    <h2>応用</h2>
    <table border="1">
      <tr v-for="data in data8" :key="data">
        <td >{{ data }}</td>
      </tr>
      <tr>
        <td><input type="text" v-model="data8_input"><button @click="button2">挿入</button></td>
      </tr>
    </table>
    テーブルにデータを追加していくサンプル。なんとv-forも変数の変化に対応する。強い。
  </section>
</template>

<script>
// componentsはimportで読み込んでおく
import radio from '@/components/timetable_radio';

export default {
  // コンポーネントを読み込む。
  // { radio }は{ radio: radio }の省略記法。
  // つまり変数名がそのままタグ名になる。
  components: {
    radio
  },
  // head内の情報。仕様上headの戻り値として定義。
  head() {
    return {
      title: "nuxtテスト", // <title>
      meta: [
        {name: 'description', content: '説明文'}
      ]
    }
  },
  // 変数の定義、オブジェクトで指定する。仕様上dataの戻り値として定義。
  data() {
    return {
      data1: "データ1",
      data2: "https://www.google.co.jp",
      data3: 1,
      data4: "",
      data5: ["a", "b", "c", "d"],
      data6: {
        foo1: "bar1",
        foo2: "bar2",
        foo3: "bar3"
      },
      data7: '',
      data8: ['a', 'b', 'c'],
      data8_input: ''
    }
  },
  // メソッドの定義
  methods: {
    button1() {
      alert("みかん");
    },
    button2() {
      // script内から変数や関数を利用する場合はthisをつける。
      this.data7.push(this.data7_input);
      this.data7_input = '';
    }
  },
  // ページ読み込み時に実行される。
  created() {

  },
  // ページが閉じられたときに実行される。
  destoryed() {

  }
}
</script>

<style lang="scss" scoped>
/* cssはここへ */
</style>
