<template>
<div id="global-layout">
    <loading v-show="isloading" />
    <live2d />
    <div class="bg" id="bg"></div>
    <component :is="layout" />
    <div class="foot"> {{$site.themeConfig.footer?$site.themeConfig.footer:'@YATING vuepress-theme-ting'}}</div>
</div>
</template>

<script>
import live2d from "../components/ting-live2d.vue";
import loading from "../components/ting-loading.vue";
export default {
    data() {
        return {
            isloading: true
        }
    },
    mounted() {
        this.isloading = false
    },
    components: {
        loading,
        live2d,
    },
    computed: {
        layout() {
            if (this.$page.path) {
                if (this.$frontmatter.layout) {
                    // 你也可以像默认的 globalLayout 一样首先检测 layout 是否存在
                    return this.$frontmatter.layout
                }
                return 'Layout'
            }
            return 'NotFound'
        }
    }
}
</script>

<style lang="stylus">
.bg {
    width 100%;
    height 100%;
    position fixed;
    z-index -8;
    background: url("../public/img/bg.jpg");
    transform: rotateY(180deg) translateX(600px);
    background-size: cover;
    background-position: center;
    opacity: .5;
}

.foot {
    text-align: center;
    font-size: 0.8em;
    margin: 0.5em;
}

#global-layout {
    max-width 900px;
    margin 0 auto;
}
</style>
