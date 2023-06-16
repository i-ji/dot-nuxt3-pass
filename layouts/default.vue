<template>
  <div>
    <main class="w-96 mx-auto mt-6 border rounded-lg shadow-[0_0_8px_#999] p-4">
      <p
        class="border rounded-sm font-['Courier_New'] text-2xl text-center py-3"
      >
        {{ result }}
      </p>
      <button
        class="w-full bg-blue-500 rounded-lg text-white py-3 mt-4 hover:opacity-60 active:opacity-40"
        @click="onPassword"
      >
        パスワードを設定
      </button>
      <fieldset
        class="border-dashed border-2 border-gray-400 rounded-lg p-4 mt-4 flex justify-between"
      >
        <legend class="px-2">オプション</legend>
        <label
          >長さ(<span class="w-6 inline-block text-center">{{ slider }}</span
          >)
          <input type="range" min="8" max="24" v-model="slider" />
        </label>
        <label
          >数字
          <input type="checkbox" v-model="numbersCheckbox" />
        </label>
        <label
          >記号
          <input type="checkbox" v-model="symbolsCheckbox" />
        </label>
      </fieldset>
    </main>
  </div>
</template>
<script setup>
import { ref } from "vue";

// スライダーの初期値
const slider = ref(8);

// パスワードの初期値
const result = ref("Push the button!!");

// 数字オプションの初期値
const numbersCheckbox = ref(false);

// 記号オプションの初期値
const symbolsCheckbox = ref(false);

// ボタン入力時のイベント内容
const onPassword = () => {
  let password = ref("");
  //   英字
  const letters = ref("abcdefghijklmnopqrstuvwxyz");
  let seed = ref(letters.value + letters.value.toUpperCase());
  //   数字
  const numbers = ref("0123456789");
  if (numbersCheckbox.value) {
    seed.value += numbers.value;
  }
  //   記号
  const symbols = ref("!#$%&()");
  if (symbolsCheckbox.value) {
    seed.value += symbols.value;
  }
  //   ループ処理
  for (let i = 0; i < slider.value; i++) {
    password.value += seed.value[Math.floor(Math.random() * seed.value.length)];
  }
  result.value = password.value;
};
</script>
