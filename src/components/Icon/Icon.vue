<template>
  <span ref="elRef" :class="[$attrs.class, 'app-iconify anticon']" :style="getWrapStyle"></span>
</template>
<script lang="ts">
  // import  { PropType } from 'vue';
  import {
    defineComponent,
    ref,
    watch,
    onMounted,
    nextTick,
    unref,
    computed,
    CSSProperties,PropType
  } from 'vue';
  import Iconify from '@purge-icons/generated';
  import { propTypes } from '../../types/propTypes';
  export default defineComponent({

    name: 'GIcon',
    props: {
      // icon name
      icon: propTypes.string,
      // icon color
      color: propTypes.string,
      // icon size
      size: {
        type: [String, Number] as PropType<string | number>,
        default: 16,
      },
      prefix: propTypes.string.def(''),
    },

    setup(props:any) {
        console.log(props.icon);
        
      const elRef = ref(null);

      const getIconRef = computed(() => {
        const { icon, prefix } = props;
        return `${prefix ? prefix + ':' : ''}${icon}`;
      });

      const update = async () => {
        const el:any = unref(elRef);
        if (el) {
          await nextTick();
          const icon = unref(getIconRef);
          if (!icon) return;
          const svg = Iconify.renderSVG(icon, {});

          if (svg) {
            el.textContent = '';
            el.appendChild(svg);
          } else {
            const span = document.createElement('span');
            span.className = 'iconify';
            span.dataset.icon = icon;
            el.textContent = '';
            el.appendChild(span);
          }
        }
      };

      watch(() => props.icon, update, { flush: 'post' });

      onMounted(update);

      const getWrapStyle = computed(
        (): CSSProperties => {
          const { size, color } = props;
          let fs = size;
          if (typeof size === 'string') {
            fs = parseInt(size, 10);
          }
          return {
            fontSize: `${fs}px`,
            color,
            display: 'inline-flex',
          };
        }
      );

      return { elRef, getWrapStyle };
    },
  });
</script>
<style >
  .app-iconify {
    display: inline-block;
    vertical-align: middle;
  }

  span.iconify {
    display: block;
    min-width: 1em;
    min-height: 1em;
    background: #5551;
    border-radius: 100%;
  }
</style>
