<script setup lang="ts">
const { size = 'size-6', text = true, textSize = 'text-base', lp = false } = defineProps<{
  size?: string
  text?: boolean
  textSize?: string
  lp?: boolean
}>()

const logo = ref<SVGSVGElement>()

function downloadLogo(svg: string, filename: string) {
  const blob = new Blob([svg], { type: 'image/svg+xml' })
  const url = URL.createObjectURL(blob)
  const link = document.createElement('a')
  link.href = url
  link.download = filename
  link.click()
  URL.revokeObjectURL(url)
  toast.success('Logo downloaded successfully')
}

const items = [
  [
    {
      label: 'Copy logo as SVG',
      icon: 'custom:shelve',
      onSelect: () => {
        copyToClipboard(logo.value!.outerHTML, 'Logo copied to clipboard')
      }
    },
    {
      label: 'Download logo',
      icon: 'lucide:download',
      onSelect: () => {
        downloadLogo(logo.value!.outerHTML, 'shelve.svg')
      }
    },
  ],
  [
    {
      label: 'Brand Assets',
      icon: 'i-heroicons-photo',
      to: 'https://shelve.cloud/brand'
    }
  ]
]
</script>

<template>
  <UContextMenu
    :items
    :ui="{
      content: 'w-48'
    }"
  >
    <div class="cursor-pointer flex items-center gap-2 text-highlighted">
      <svg ref="logo" xmlns="http://www.w3.org/2000/svg" :class="size" fill="currentColor" viewBox="0 0 717 488">
        <path
          d="M700.867 0L577.808 142.717C563.922 158.728 542.573 168.197 519.836 168.197H388.098C379.94 168.197 373.518 162.343 373.518 155.113V110.696C373.518 98.3011 355.814 92.9643 347.309 102.777L182.593 293.698C168.708 309.709 147.359 319.177 124.622 319.177H0L253.583 25.4791C267.468 9.46859 288.817 0 311.554 0H700.867Z"
        />
        <path
          d="M15.4475 487.374L138.507 344.657C152.393 328.646 173.742 319.177 196.479 319.177H328.217C336.375 319.177 342.797 325.031 342.797 332.261V376.678C342.797 389.073 360.501 394.41 369.005 384.597L533.721 193.676C547.607 177.665 568.956 168.197 591.693 168.197H716.141L462.559 461.895C448.673 477.905 427.324 487.374 404.587 487.374H15.4475Z"
        />
      </svg>
      <NuxtLink v-if="text" to="/" aria-label="Shelve" class="max-sm:hidden font-semibold" :class="textSize">
        Shelve
      </NuxtLink>
    </div>
  </UContextMenu>
</template>
