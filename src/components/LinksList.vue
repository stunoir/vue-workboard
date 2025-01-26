<script setup>
  const tools = [
    { name: 'password generator', url: 'https://www.avast.com/en-gb/random-password-generator' },
    { name: 'kraken', url: 'https://kraken.io/web-interface' },
    { name: 'jpg to svg', url: 'https://pixelied.com/convert/jpg-converter/jpg-to-webp' },
    { name: 'svg url encoder', url: 'https://yoksel.github.io/url-encoder/' },
    { name: 'shadow generator', url: 'https://getcssscan.com/css-box-shadow-examples' },
    { name: 'favicon generator', url: 'https://realfavicongenerator.net/' },
    { name: 'icon finder', url: 'https://www.iconfinder.com/' },
    { name: 'icomoon', url: 'https://icomoon.io/' },
    { name: 'md to html', url: 'https://markdowntohtml.com/' },
    { name: 'html editor', url: 'https://html5-editor.net/' }
  ]
</script>

<template>
  <div class="component-container">
    <h3 class="text-md">Tools</h3>
    <div class="flex-container flex-gap-10">
      <a
        v-for="tool in tools"
        :key="tool.name"
        class="btn-main btn-main--ghost btn-main--xs"
        :href="tool.url"
        target="_blank"
      >
        {{ tool.name }}
      </a>
    </div>
  </div>
</template>
