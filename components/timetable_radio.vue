<template>
    <!-- 基本的には普通のページと一緒。 -->
    <label>
        <input type="radio" :value="value" :checked="value === model" :name="name" @change="$emit('change', value)">
        <svg xmlns="http://www.w3.org/2000/svg" width="255.426" height="48" viewBox="0 0 255.426 48">
            <polygon class="left_hexagon" points="13.856,0 41.569,0 55.426,24 41.569,48 13.856,48 0,24" />
            <polyline class="line topline" points="41.569,1 240.703,1 254.271,24 253.164,25" />
            <polyline class="line borromline" points="41.569,47 240.703,47 254.271,24 253.164,23" />
        </svg>
        <!--
            slot要素
            このコンポーネントがradioだとして、
            <radio>文字列</radio>
            の「文字列」の部分がここに表示される。
        -->
        <div class="label"><slot/></div>
    </label>
</template>

<style lang="scss" scoped>
label {
    display: inline-block;
    position: relative;
    width: 255.426px;
    height: 48px;
    cursor: pointer;

    -webkit-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
            user-select: none;
}

input {
    display: none;
}

svg {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}

.left_hexagon {
    fill: #ee7836;
}
.line {
    fill: transparent;
    stroke: #ee7836;
    stroke-width: 2;
    stroke-dasharray: 227.330;
    stroke-dashoffset: 227.330;

    transition-property: stroke-dashoffset;
    transition-duration: 0.5s;
    transition-timing-function: cubic-bezier(0, 0, 0.1, 1);
}

:checked + * .line {
    stroke-dashoffset: 0;
}

.label {
    position: absolute;
    left: 41.569px;
    right: 13.857px;
    top: 50%;
    transform: translateY(-50%);
    text-align: center;
}
</style>

<script>
export default {
    /*
    props
    属性はここで読み取れるようになる。
    たとえばnameを指定しておけば
    <radio name="test"></radio>
    のtestが変数nameで読み取れる。
    指定方法がいくつかあり
    ・配列で属性名を列挙する。
    ・オブジェクトで変数名と型を列挙する(ここではこれを使用)

    */
    props: {
        value: String,
        model: String,
        name: String
    },
    /*
    model
    v-modelをこのコンポーネントに指定したときにどの変数と連動させるか指定する。
    ついでに変化したときに発火するイベント名も設定できる。
    */
    model: {
        prop: 'model',
        event: 'change'
    }
}
</script>