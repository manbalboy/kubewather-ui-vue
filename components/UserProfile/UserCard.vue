<template>
  <Card class="card-user">
    <p class="card-text"></p>
    <div class="author">
      <div class="block block-one"></div>
      <div class="block block-two"></div>
      <div class="block block-three"></div>
      <div class="block block-four"></div>
      <a href="javascript:void(0)">
        <!--        <img class="avatar" src="img/emilyz.jpg" alt="..." />-->
        <h5 class="title">Mike Andrew</h5>
      </a>
      <p class="description">Ceo/Co-Founder</p>
    </div>
    <p></p>
    <div class="card-description">
      Do not be scared of the truth because we need to restart the human foundation in truth And I love you like Kanye
      loves Kanye I love Rick Owens’ bed design but the back is...
    </div>

    <div slot="footer" class="button-container">
      <BaseButton class="btn-facebook" icon round>
        <i class="fab fa-facebook"></i>
      </BaseButton>
      <BaseButton class="btn-twitter" icon round>
        <i class="fab fa-twitter"></i>
      </BaseButton>
      <BaseButton class="btn-google" icon round>
        <i class="fab fa-google-plus"></i>
      </BaseButton>
    </div>
  </Card>
</template>
<script>
  import { Card, BaseButton } from '@/components/index';
  export default {
    name: 'UserCard',
    components: {
      Card,
      BaseButton,
    },
  };
</script>
<style></style>
