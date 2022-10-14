# Introduction - problems of CNNs

### Example
<div class="text-center pt-3">
  Input: <BlockOfWord>I live in Bangkok for 4 years. It is a long time that I live here</BlockOfWord>

  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
  </svg>


  <p class="mb-0">
    Layer 1:
    <BlockOfWord>I live in&nbsp;</BlockOfWord>
    <BlockOfWord>live in <span class="text-red">Bangkok</span>&nbsp;</BlockOfWord>
    <BlockOfWord>in <span class="text-red">Bangkok</span> for&nbsp;</BlockOfWord>
    <BlockOfWord><span class="text-red">Bangkok</span> for 4&nbsp;</BlockOfWord>
    <BlockOfWord>for 4 years.&nbsp;</BlockOfWord>
    <BlockOfWord>4 years. It&nbsp;</BlockOfWord>
    <BlockOfWord>years. It is&nbsp;</BlockOfWord>
    <BlockOfWord>It is a&nbsp;</BlockOfWord>
    <BlockOfWord>is a long&nbsp;</BlockOfWord>
    <BlockOfWord>a long time&nbsp;</BlockOfWord>
    <BlockOfWord>long time that&nbsp;</BlockOfWord>
    <BlockOfWord>time that I&nbsp;</BlockOfWord>
    <BlockOfWord>that I live&nbsp;</BlockOfWord>
    <BlockOfWord>I live <span class="text-red">here</span>&nbsp;</BlockOfWord>
    <BlockOfWord>live <span class="text-red">here</span>&nbsp;</BlockOfWord>
    <BlockOfWord><span class="text-red">here</span>&nbsp;</BlockOfWord>
  </p>
  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 my-0">
    <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 110-1.5.75.75 0 010 1.5zM12 12.75a.75.75 0 110-1.5.75.75 0 010 1.5zM12 18.75a.75.75 0 110-1.5.75.75 0 010 1.5z" />
  </svg>


  <span class="block text-bold text-large mt-3">Problems: A lot of layers required to pass before process <span class="text-red">Bangkok</span> and <span class="text-red">here</span> together</span>
</div>

<style>
.block{
  display: block;
}
.my-0{
  margin: 0 auto !important;
}
.mt-3{
  margin-top: 3rem;
}
.mb-0{
  margin-bottom: 0;
}
.pt-3{
  padding-top: 3rem;
}
svg{
  display: block;
  margin: 20px auto;
}
.text-large{
  font-size: 1.5rem;
}
.text-red{
  color: red;
}
.text-bold{
  font-weight: bold;
}
</style>