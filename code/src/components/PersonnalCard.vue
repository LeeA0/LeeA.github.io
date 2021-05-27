<template>
  <div>
    <h3>{{ user.name }}</h3>
    <div class="data"><strong>이메일:</strong> {{ user.email }}</div>
    <!-- <div class="data"><strong>Phone:</strong> {{ user.phone }}</div> -->
    <div class="data"><strong>거주도시:</strong> {{ user.city }}</div>
    <!-- <div class="data"><strong>Languages:</strong> {{ user.lang }}</div> -->
    <div class="data"><strong>생년월일:</strong> {{ user.birth }}</div>
    <SocialBar :links="links"/>
  </div>
</template>

<script>
import SocialBar from './SocialBar.vue'

export default {
    name: 'PersonnalCard',
    props: ['user', 'links'],
    components: {
        SocialBar,
    }
}
</script>

<style scoped lang="scss">
    @import '@/styles/constants.scss';

    .data {
        margin-bottom: 15px;
    }
</style>