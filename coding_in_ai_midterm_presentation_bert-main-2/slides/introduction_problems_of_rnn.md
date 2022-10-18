# Introduction - problems of RNN

### Example
<div class="text-center pt-3">
  Input: <span>I live in Bangkok for 4 years. It is a long time that I live here</span>

  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
  </svg>


  <p class="mb-0">
    <span class="gradient-gray-black">I live in Bangkok for 4 years. It is a long time that I live here</span>
  </p>


  <span class="block text-bold text-large mt-3">Problems: A lot of itteration from <span class="text-red">Bangkok</span> to <span class="text-red">here</span></span>
</div>

<style>
.gradient-gray-black{
  background-color: #000;
  background-image: linear-gradient(45deg, #999, #000);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
svg{
  display: block;
  margin: 20px auto;
}
</style>
