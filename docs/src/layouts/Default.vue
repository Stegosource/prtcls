<template>
  <div>
    <header class="flex justify-content-between p-4 border-b-1 border-gray-2">
      <g-link to="/">
        <img
          src="/img/icon.svg"
          :alt="$static.metadata.siteName"
          width="32"
          height="40"
          class="mr-1"
        />
        <span class="visually-hidden">Particles CSS</span>
        <span>v{{ $options.version }}</span>
      </g-link>

      <a href="https://github.com/stegosource/prtcls">
        <PSvg icon="icon-github" class="size-6" />
        <span class="visually-hidden">GitHub</span>
      </a>
    </header>

    <div class="layout-default grid gap-4 align-items-start my-10 mx-auto px-4">
      <aside class="sticky top-0 border-1 border-gray-2 p-4 bg-white">
        <nav>
          <h3>Sections</h3>
          <ul class="nav">
            <li v-for="(link, i) in $options.links" :key="i">
              <g-link :to="link.to">{{ link.text }}</g-link>
            </li>
          </ul>
        </nav>
      </aside>

      <main class="w-full max-w-15 mx-auto">
        <slot />

        <section
          v-for="slot of slotKeys"
          :key="slot"
          :id="`${slot}`"
          class="mt-12 first:mt-0"
        >
          <slot :name="slot" />
        </section>
      </main>

      <aside
        v-if="slotKeys.length"
        class="sticky top-0 border-1 border-gray-2 p-4 bg-white"
      >
        <h4>On this page</h4>
        <ul class="capitalize">
          <li v-for="slot of slotKeys" :key="slot">
            <a :href="`#${slot}`">{{ slot }}</a>
          </li>
        </ul>
      </aside>
    </div>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import pkg from "../../../package.json";

export default {
  data: () => ({
    drawer: false
  }),

  version: pkg.version,

  links: [
    {
      text: "About",
      to: "/"
    },
    {
      text: "Display",
      to: "/display/"
    },
    {
      text: "Opacity",
      to: "/opacity/"
    },
    {
      text: "Visibility",
      to: "/visibility/"
    },
    {
      text: "Position",
      to: "/position/"
    },
    {
      text: "Grid",
      to: "/grid/"
    },
    {
      text: "Flexbox",
      to: "/flexbox/"
    },
    {
      text: "Align & Justify",
      to: "/align-justify/"
    },
    {
      text: "Width & Height",
      to: "/width-height/"
    },
    {
      text: "Overflow",
      to: "/overflow/"
    },
    {
      text: "Margin & Padding",
      to: "/margin-padding/"
    },
    {
      text: "Border",
      to: "/border/"
    },
    {
      text: "Font",
      to: "/font/"
    },
    {
      text: "Text",
      to: "/text/"
    },
    {
      text: "Color",
      to: "/color/"
    },
    {
      text: "Background",
      to: "/background/"
    }
  ],

  computed: {
    slotKeys() {
      return Object.keys(this.$slots).filter(key => key !== "default");
    }
  }
};
</script>

<style lang="scss">
.layout-default {
  grid-template-columns: auto 1fr auto;
}
</style>
