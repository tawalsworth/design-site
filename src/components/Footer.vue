<template>
<div class="footerBackground">
  <footer>
      <p className={FooterStyles.footer__copyright}>
        © {Config.site.owner} {date.getFullYear()} All Rights Reserved.
      </p>
  </footer>
</div>
</template>

<script>
    export default{

      }
</script>

<style>
.footerBackground{
  background-color: black;
}
footer{
  color: white; 
}

</style>