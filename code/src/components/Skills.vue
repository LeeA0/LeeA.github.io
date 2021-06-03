<template>
    <section id="skills">
        <AnimateOnVisible name="fadeDown" :duration="1">
            <Title :title="content.metadata.title" :description="content.metadata.description" />
        </AnimateOnVisible>

        <div class="section-content">
            <div class="full-width">
                <div class="row justify-center">
                    <div class="col-md-2 col-xs-12 q-m-auto q-pb-4" v-for="(post, index) in this.content.metadata.items" :key="index">
                        <AnimateOnVisible name="bounce">
                            <q-img id="imgLogo" class="q-mx-auto" :src="getImgUrl(post.img)" :alt="post.title"/>
                            <div id="divAlt" class="altCaption text-center">{{post.title}}</div>
                        </AnimateOnVisible>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    import Title from './Title.vue'

    export default {
        name: 'Skills',
        components: {
            Title,
        },
        props: ['content'],
        methods: {
            getImgUrl(img) {
                return require('../assets/img/logo/'+img);
            },
        },
    }
</script>

<style scoped lang="scss">
    @import '@/styles/constants.scss';

    #skills {
        background-color: lighten(map-get($colors, dark), 100%);
    }

    @media(min-width: #{map-get($breakpoints, medium)}) {
        .section-content {
            width: 80%;
            margin: 0 auto;
        }
    }

    #imgLogo{
        max-width: 120px;
        display: block;
    }

    .altCaption{
        color: map-get($colors, secondary);
        margin-top: 1rem;
    }
</style>