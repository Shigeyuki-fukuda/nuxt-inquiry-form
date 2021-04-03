<template>
  <div class="flex items-center min-h-screen bg-black">
    <div class="container mx-auto">
      <div class="max-w-md mx-auto my-10 bg-white p-5 rounded-md shadow-sm">
        <div class="text-center">
          <h1
            class="my-3 text-3xl font-semibold text-gray-700 dark:text-gray-200"
          >
            お問い合わせ
          </h1>
        </div>
        <div class="m-7">
          <form>
            <div class="mb-6">
              <label
                for="name"
                class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >
                お名前
                <span class="text-xs text-red-500">(必須)</span>
              </label>
              <input
                id="name"
                type="text"
                name="name"
                placeholder="お名前太郎"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              />
            </div>
            <div class="mb-6">
              <label
                for="email"
                class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >
                メールアドレス
                <span class="text-xs text-red-500">(必須)</span>
              </label>
              <input
                id="email"
                type="email"
                name="email"
                placeholder="your@example.com"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              />
            </div>
            <div class="mb-6">
              <label
                for="phone"
                class="text-sm text-gray-600 dark:text-gray-400"
              >
                電話番号
              </label>
              <input
                id="phone"
                type="text"
                name="phone"
                placeholder="0312345678"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              />
            </div>
            <div class="mb-6">
              <label
                for="message"
                class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >
                内容
                <span class="text-xs text-red-500">(必須)</span>
              </label>
              <textarea
                id="message"
                rows="5"
                name="message"
                placeholder="お問い合わせ内容です"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              >
              </textarea>
            </div>
            <div class="mb-6">
              <button
                type="submit"
                class="w-full px-3 py-4 text-white bg-indigo-500 rounded-md focus:bg-indigo-600 focus:outline-none"
              >
                送信する
              </button>
            </div>
            <p id="result" class="text-base text-center text-gray-400"></p>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
