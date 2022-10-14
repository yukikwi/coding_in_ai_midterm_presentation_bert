---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center, h-5/7, mx-auto, flex, items-center, my-3'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Coding in AI midterm presentation
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---

# How to Fine-Tune BERT for Text Classification

Coding in AI Midterm exam presentation

---

# Contents

- **Introduction**
- **Theory**
- **Experimental Design and Results**
- **Conclusion**

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Introduction

<img src="introduction.png" />
<span>But why not used CNNs & RNN?</span>

<style>
img {
  max-width: 80%;
  margin: auto;
}
span {
  text-align: center;
  width: 100%;
  display: block;
}
</style>

---
preload: false
src: ./slides/introduction_problems_of_cnns.md
---
---
src: ./slides/introduction_problems_of_rnn.md
---
---

# Introduction - How transformer fix this

> Transformer คือ architecture ทาง NLP ที่ออกแบบมาเพื่อแก้ปัญหาของ CNNs และ RNN โดยใช้สิ่งที่เรียกว่า Self-Attention ซึ่งเป็นการให้ความสำคัญกับความสัมพันธ์ระหว่างคำในประโยค

<img src="self_attention.png" />

<style>
  img{
    max-height: 70%;
    margin: 20px auto;
  }
</style>

---

# Introduction - What is BERT

> BERT หรือ Bidirectional Encoder Representations from Transformers เป็น model ที่ถูกพัฒนาโดยใช้ encoder ของ transformer โดยมีจุดประสงค์คือเพื่อเป็น language model ซึ่งจัดเป็น state-of-the-art language model โดย base model ถูกออกแบบมาเพื่อ predict คำที่หายไป

<img src="bert.webp" />

<style>
  img{
    max-height: 70%;
    margin: 20px auto;
  }
</style>

---

# Theory

  - Language Model Pre-training
  - Multi-task learning
  - BERT for Text Classification

---

# Theory - Language Model Pre-training
> language model ที่ผ่านการเรียนรู้มาแล้วด้วยข้อมูลมาแล้ว โดยในงานวิจัยนี้ได้เลือกใช้ **BERT Pre-training model** ซึ่งเป็นโมเดลแบบ **Unsupervised Learning** ที่เรียนรู้ผ่านชุดข้อมูลที่ใช้ไม่จำเป็นต้องมี Label อะไร 

<div class="flex h-5/7 my-3">
  <img class="mx-auto content-center" src="pre_trained.png" />
</div>
---

# Theory - Multi-task learning
> เป็นการ **Share layers** ของโมเดลในการทำ **Task ที่แตกต่างกัน**ทำให้โมเดลไม่จำเป็นต้องเรียนรู้ใหม่ตั้งแต่เริ่มต้น ซึ่งมีส่งผลต่อประสิทธิภาพทำให้ประหยัดเวลาและทรัพยากรในการประมวลผล ในงานวิจัยฉบับนี้ได้ใช้ **BERT Pre-training model** เป็น Multi-task learning ในการ Share Pre-traning model

<div class="flex h-5/7 my-3">
  <img class="mx-auto content-center" src="multitask_learning.png" />
</div>

---

# Theory - BERT for Text Classification
> เป็นการ **Share layers** ของโมเดลในการทำ **Task ที่แตกต่างกัน**ทำให้โมเดลไม่จำเป็นต้องเรียนรู้ใหม่ตั้งแต่เริ่มต้น ซึ่งมีส่งผลต่อประสิทธิภาพทำให้ประหยัดเวลาและทรัพยากรในการประมวลผล ในงานวิจัยฉบับนี้ได้ใช้ **BERT Pre-training model** เป็น Multi-task learning ในการ Share Pre-traning model

> โดยจะมีการใช้ Softmax เป็น activation function ใน layer สุดท้ายเพื่อทำ classification โดยจะทำการคำนวนจาก hidden state ของ token **[CLS]** ดังสมการ

<img class="size-content mx-auto" src="equation_softmax.png" />

<div class="mx-auto w-fit">
  <ul>
    <li>W: weight</li>
    <li>h: Hidden state</li>
  </ul>
</div>

<style>
  .w-fit{
    width: fit-content;
  }
  .size-content {
    width: fit-content;
    height: fit-content;
  }
</style>
---

# Experimental Design and Results
  - Methadology
  - Dataset
  - Data preprocessing
  - Hyperparameters

---

# Experimental Design and Results - Methadology
ในการทำ fine-tune BERT จะมีสิ่งที่ต้องคำนึง 3 ส่วนได้แก่
  - 1. Fine-Tuning Strategies: เป็นการหาวิธีที่เหมาะสมในการ fine tune model
    - 1.1. pre process ข้อความไม่ให้ยาวเกิน 512
    - 1.2. ต้องเลือก layer ที่มีประสิทธิภาพในการทำ text classification มากที่สุด
    - 1.3. ต้องเลือก optimizers และ learning rate ให้เหมาะสมเพื่อป้องกันการ overfit

  - 2. Further Pre-training: เป็นการให้โมเดลเรียนรู้ข้อมูลที่อยู่ใน Target domain เพิ่มเติมเพื่อให้โมเดลมีความสามารถแยกแยะข้อความมากขึ้น
    - 2.1 Within-task pre-training: ใช้  Pre-training model เรียนรู้เพิ่มกับชุดข้อมูลเดิมแต่เป็น Target Task
    - 2.2 In-domain  pre-training: หลักจากที่ทำการ Pre-training model เรียนรู้กับ Target Task เพิ่มเติมแล้วต้องทดสอบกับ Tarket Task ที่หลากหลายมากขึ้นแต่ยังคงเป็นชุดข้อมูลเดิมอยู่
    - 2.3 Cross-domain pre-training: เรียนรู้กับข้อมูลชุดใหม่ที่ Target Task ไม่มีความสำคัญเกี่ยวข้องชุดข้อมูลก่อน
หน้านี้เลยรวมกับชุดที่เคยเรียนแล้ว

---

# Experimental Design and Results - Methadology
  - 3. Multi-Task Fine-Tuning: เนื่องจากหัวข้อ Multi-task learning งานวิจัยนี้ได้ทำการ Share Layer ในการทำ Task ที่แตกต่างกันซึ่งสอดคล้องกับงานวิจัยของเราที่มีการเปลี่ยน task ของโมเดล BERT จากการ predict คำมาเป็น text classification

---

# Experimental Design and Results - Dataset

ในงานวิจัยนี้ได้มีการเลือกใช้ datasets ทั้งหมด **8 datasets** เพื่อครอบคลุม 3 common text classification อันได้แก่

  - 1. Sentiment analysis
    - 1.1 dataset binary film review IMDb dataset (Maas et al., 2011)
    - 1.2 five-class version of the Yelp review dataset built by Zhang et al. (2015)
    - 1.3 binary version of the Yelp review dataset built by Zhang et al. (2015)
  - 2. Question classification
    - 2.1 dataset six-class version of the TREC dataset (Voorhees and Tice, 1999)
    - 2.2 Yahoo!
    - 2.3 dataset คำตอบที่ถูกสร้างโดย Zhang et al. (2015)
  - 3. Topic classification
    - 3.1 dataset large-scale AG’s News และ DBPedia created et Zhang et al. (2015).
    - 3.2 dataset from Sougou news corpus

---

# Experimental Design and Results - Data preprocessing

งานวิจัยนี้ได้มีการใช้ **WordPiece embedding** โดยทำการแบ่งเป็น **30,000 token** และทำการแบ่งคำโดยใช้สัญลักษณ์ **##**  และสำหรับการแบ่งประโยคจะใช้ **spaCy** สำหรับภาษาอังกฤษ และ **“。”, “? ”, “! ”** สำหรับภาษาจีน

#### Example
  - Monkey##climb##a##tree
  - I##live##in##Bangkok

---

# Experimental Design and Results - Hyperparameters

งานวิจัยนี้ได้มีการใช้ **BERT base model** มาทำการ fine tune ด้วย parameters ดังต่อไปนี้

  - batch size = 24
  - dropout propability = 0.1 (fixed)
  - optimizer = Adam (β1 = 0.9, β2 = 0.999)
  - learning rate scheduler = Slanted triangular learning rate (initial learning rate = 2e-5)
  - warm-up proportion = 0.1
  - max epoch = 4 โดยจะทำการเลือก model ที่ดีที่สุดจาก validation set

---

# Experiments
  - Exp-I: Investigating Different Fine-Tuning Strategies