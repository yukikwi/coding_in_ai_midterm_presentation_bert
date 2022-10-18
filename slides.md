---
# try also 'default' to start simple
theme: seriph
# apply any windi css classes to the current slide
class: 'text-center, h-5/7, mx-auto, flex, items-center'
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
- **Experiments**
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
img {
  max-height: 70%;
  margin: 20px auto;
}
</style>

---

# Introduction - What is Token

> Transformer จะทำการเปลี่ยนประโยคไปเป็น token ก่อน เพื่อให้สะดวกต่อการทำงาน โดย Transformer จะทำการ break sentence ออกมาเป็น token จากนั้นจึงเพิ่ม token [CLS] และ [SEP] ที่ต้นและท้ายประโยค ก่อนจะนำไปคำนวณ id

<img src="bert_tokenize.png" />

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

<style>
  .my-3{
    margin-top: 0.75rem;
    margin-bottom: 0.75rem;
  }
</style>

---

# Theory - Multi-task learning
> เป็นการ **Share layers** ของโมเดลในการทำ **Task ที่แตกต่างกัน**ทำให้โมเดลไม่จำเป็นต้องเรียนรู้ใหม่ตั้งแต่เริ่มต้น ซึ่งมีส่งผลต่อประสิทธิภาพทำให้ประหยัดเวลาและทรัพยากรในการประมวลผล ในงานวิจัยฉบับนี้ได้ใช้ **BERT Pre-training model** เป็น Multi-task learning ในการ Share Pre-traning model

<div class="flex h-5/7 my-3">
  <img class="mx-auto content-center" src="multitask_learning.png" />
</div>

<style>
  .my-3{
    margin-top: 0.75rem;
    margin-bottom: 0.75rem;
  }
</style>

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
    - 2.1 Within-task pre-training
    - 2.2 In-domain  pre-training
    - 2.3 Cross-domain pre-training

---

# Experimental Design and Results - Methadology
  - 3. Multi-Task Fine-Tuning: เนื่องจาก task ของ BERT คือการ predict missing word ดังนั้นเราต้อง fine-tune model ให้ fit กับ task ของเรา

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

งานวิจัยนี้ได้มีการใช้ **WordPiece embedding** โดยทำการแบ่งเป็น **30,000 token**
- word: แบ่งโดยใช้สัญลักษณ์ **##**
- sentence: ใช้ **spaCy** สำหรับภาษาอังกฤษ และ **“。”, “? ”, “! ”** สำหรับภาษาจีน

<br />

#### **Example**
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

 1. ชุดทดสอบ: **IMDb dataset** 
    - จุดประสงค์ในการทดสอบที่ 1 : **ทดสอบ Pre-train BERT Strategies**
    - ขั้นตอนในการในการทดสอบ
      - การทดสอบ Pre-train BERT Strategies 1 : การจัดการกับข้อความที่ยาวเกินกว่า 512 tokens 
        - <font color="salmon">Truncation methods </font> ซึ่งแนวคิดของวิธีนี้คือใจความสำคัญของประโยคนั้น จะอยู่ที่ต้นและท้ายประโยค จึงสามารถแบ่งวิธีการ truncate ได้อีก 3 วิธีย่อย ได้แก่
          - head-only: ใช้เฉพาะ 510 token แรก
          - tail-only: ใช้เฉพาะ 510 token หลัง
          - head + tail: ใช้ 128 token แรก และ 382 token หลัง
        - การทดสอบที่ 2 : <font color="salmon"> Hierarchical methods </font> แนวคิดที่จะทำการแบ่งข้อความเป็น Fraction 
          - ช่วงที่หนึ่งจะแบ่งเป็น k = L/510 fractions แล้วจึงนำแต่ละ fraction ไปผ่าน BERT model โดยผลลัพธ์จะอยู่ที่ hidden state ของ [CLS] 
          - ช่วงที่สองจำผลลัพธ์ไปทำ max pooling และ self attention แล้วทำการรวมผลลัพธ์จากทุก fractions
        
---

- ผลการทดสอบ Exp-I: dารจัดการกับข้อความที่ยาวเกินกว่า 512 tokens 

<img class="size-content mx-auto" src="Result_Dealing_with_long_texts.png"/>

<style>
  .w-fit{
    width: fit-content;
  }
  .size-content {
    width: fit-content;
    height: fit-content;
  }
</style>

> จากการทดสอบด้วยชุดข้อมูล IMDb dataset และ Sogou (Chinese Sogou News Datasets ) ว่า Truncation methods, head + Tail ให้ผลลัพธ์ Test error rates (%) ที่ต่ำที่สุดจากทั้งสองชุดข้อมูล

---

- การทดสอบ Pre-train BERT Strategies 2 : **Feature From Differrent layers**
ขั้นตอนการจัดการกับ Features จาก layer ที่แตกต่างกันเนื่องจากในงานวิจัยนี้มีแนวคิดว่า layer ที่ต่างกันจะให้ feature ของประโยคที่แตกต่างกัน**

 - ผลการทดสอบ Pre-train BERT Strategies 2: 

  <img src="Result_Fine_tuning_BERT_with_different_layers.png"/>

<style>
img{
  max-height: 60%;
  margin: 20px auto;
}
</style>

> จากผลลัพธ์ที่ได้คือ Layer-11 (layer สุดท้ายของ transformers encoder)  ให้ผลลัพธ์ Test error rates(%) ที่ต่ำที่สุด

---

- การทดสอบ Pre-train BERT Strategies 3 : **Catastrophic forgetting**
ขั้นตอนการการจัดการปัญหาที่โมเดลลืมข้อมูลที่ pre-trained มาแล้ว หรือ Catastrophic forgetting**

  ขั้นตอนในการในการทดสอบ <font color="salmon">ปรับ Learning rate</font> 

  <img src="Resualt_test_result.png"/>

<style>
  img{
    max-height: 70%;
    margin: 20px auto;
  }
</style>

  > 2e-5 จะช่วยให้โมเดลไม่เกิด Error rate สูงแต่ถ้าหากค่า learning rate สูงเช่น 4e-4 จะพบปัญหา Error rate

---
class: 'grid, grid-cols-2'
---
- การทดสอบ Pre-train BERT Strategies 4 : **Layer-wise decreasing layer rate**

  ขั้นตอนในการในการทดสอบ <font color="salmon">การหาค่า Decay factor learning rate ที่ที่จะให้ Error rate น้อยและส่งผลต่อประสิทธิภาพ </font> 
  
  <div class="grid grid-cols-2">
    <div>
      <img src="Result_decay_factor.png"/>
    </div>
    <div>

  ```python
    def decay_factor(learning_rate, decay_factor, iters):
     return learning_rate * (1/1 + decay_factor * iters)
  ```

    </div>
  </div>

  > การกำหนดให้ layer ชั้นเริ่มต้นให้มีค่า learning rate น้อยๆ นั้นมีประสิทธิภาพและที่ Learning rate = 2.0e-5 และ decay factor = 0.95 นั้นให้ค่า error rate ที่ต่ำที่สุด

<style>
  img{
    height: 25vh;
    margin: 20px auto; 
  }
  code {
    font-size: 12px;
  }
</style>

--- 

# Experiments
  - Exp-II: Investigating the Further Pretraining

    - 1. จุดประสงค์ในการทดสอบที่ 2 หลังจากได้ทดสอบทดสอบปัญหาและหาค่า Hyperparameter ที่ให้ผลดีกับโมเดลในการทายประโยคถัดไปด้วย BERT Pre-training model แล้ว **การทดลองที่ 2 นี้จะเกี่ยวกับการปรับโมเดลจากการทายคำที่ขาดหายไปให้ใช้งานได้สำหรับการทำ Text Classification**
    - 2. ขั้นตอนในการในการทดสอบ
      - <font color="salmon">Within-Task Further Pre-Training</font> 
        ใช้ BERT Pre-training model (BERT) เรียนรู้เพิ่มกับชุดข้อมูลเดิมแต่เป็น Target Task (Within-Task Pre-Training) (ITPT) และผลลัพธ์การ Fine-tune model (FiT) จากการทดลองที่หนึ่งทั้งหมด 100K Training Step (BERT-ITPT-FiT)

      - <font color="salmon">In-Domain and Cross-Domain Further Pre-Training</font> 
        ใช้ BERT Pre-training model เรียนรู้กับ Target Task เพิ่มเติม โดยผู้วิจัยได้ใช้ seven English datasets แบ่งเป็นสามโดเมน ประกอบด้วย topic, sentiment และ question หลังจากนั้นเรียนรู้กับข้อมูลชุดใหม่ที่ Target Task ไม่มีความสำคัญเกี่ยวข้องกับชุดข้อมูล
      ก่อนหน้านี้เลยทั้งหมด 7 ชุดข้อมูลทดสอบ

---

# Experiments
- Exp-II: Investigating Different Fine-Tuning Strategies

  - 2. ขั้นตอนในการในการทดสอบ (ต่อ)
    - <font color="salmon">Comparisons to Previous Models</font>
      ผู้วิจัยได้ทำการเปรียบเทียบโมเดลโดยแต่ละโมเดลมีจุดประสงค์ที่แตกต่างกัน โดยเฉพาะ ULMFiT ซึ่งเป็น state-of-art สำหรับการทำ Text-Classification กับโมเดล BERT ที่ผู้วิจัยได้พัฒนาขึ้นประกอบไปด้วย

      - BERT-Feat (“BERT as features” เป็นโมเดลที่ใช้ BERT เป็น input embedding ของ biLSTM ร่วมกับ self-attention)
      - BERT-Fit (BERT + fine tuning)
      - BERT-ITPT-Fit (BERT + withIn-Task Pre-Training + Fine tuning)
      - BERT-IDPT-Fit (BRTT + In-Domain Pre-Training + Fine tuning)
      - BERT-CDPT-Fit (BERT + Cross-Domain Pre-Training + Fine tuning)

---

ผลการทดสอบ Exp-II: Within-Task Further Pre-Training

<img src="Within_Task_Further_Pre_Training.png"/>

> ผลลัพธ์จากการ Fine-tune model (FiT) พบว่าการทดสอบทั้งหมด 100K Training Step (BERT-ITPT-FiT) ให้ผลลัพธ์ Test error (%) น้อยที่สุด

<style>
  img {
    max-height: 70%;
    margin: 20px auto;
  }
</style>

---

ผลการทดสอบ Exp-II: Investigating the Further Pre-training

<img src="In_Domain_and_Cross_Domain_Further_Pre_Training.png"/>

> All further pre-training (row ‘all’ in Table) ให้ผลลัพธ์ที่ดีกว่าการทำ BERT-base Model 
  (row ‘w/o pretrain’ in table), สำหรับโดเมน Question ชุดข้อมูล TREC ที่มีขนาดเล็กมีประสิทธิภาพที่แย่มากแต่เมื่อใช้ชุดข้อมูล Yah. A ประสิทธิภาพจะดีที่สุด และการทำ Cross-domain pre-training (row ‘all’ in Table) ไม่ได้ทำให้เกิดประสิทธิภาพที่ดีให้กับโดเมน topic, sentiment และ question เลย เนื่องจากโมเดลทำงานได้ดีตั้งแต่ทดสอบกับโดเมนเริ่มต้นแล้ว
  

<style>
img {
  max-height: 50%;
  margin: 20px auto;
}
</style>

---

ผลการทดสอบ Exp-II: Comparisons to Previous Models :

<img src="Result_Comparisons_to_Previous_Models.png"/>

<style>
  img{
    max-height: 50%;
    margin: 20px auto;
  }
</style>

--- 

# Experiments
  - Exp-III: Multi-task Fine Tuning

  1. จุดประสงค์ในการทดสอบที่ 3 **Share Layer ในการทำ Task ที่แตกต่างกัน ด้วยใช้ 4 ชุดข้อมูล**
  2. ข้อมูลที่ใช้ในการทดสอบ
    - IMDb, Yelp P., AG และ DBP

  <img src="Result_Multitask.png"/>

<style>
  img{
    max-height: 50%;
    margin: 20px auto;
  }
</style>

> จากตารางพบว่า BERT-CDPT-FiT และ BERT-CDPT-MFit-Fit หรือ โมเดล BERT ที่ผ่านการทำ Multi-task โดยผ่าน In-Domain และ Cross-Domain (‘all sentiment’, ‘all question’, ‘all topic’) จากนั้นทำการ Fine-tuning ส่งผลให้ Test error rates ลดลง แต่ถ้าหากโมเดลที่ผ่านการ Multi-task หรือ Fine-tuning ไม่ส่งผลให้ Test error rates ลดลงเลยในทุกกรณี

--- 

  # Experiments
  - Exp-IV: Few-Shot Learning
  1. จุดประสงค์ในการทดสอบที่ 4 **ทดสอบ Pre-training model ดูว่าสามารถทำงานได้ดีกับชุดข้อมูลขนาดเล็กหรือไม่**

  2. ข้อมูลที่ใช้ในการทดสอบ IMDb Dataset โดยใช้ข้อมูลแต่ 40% 

  <img src="Result_EXP4.png"/>

<style>
  img{
    max-height: 50%;
    margin: 20px auto;
  }
</style>

  > จากผลลัพธ์จะเห็นว่า Test error rates สำหรับการทำ Further pre-trained BERT สามารถเพิ่มประสิทธิภาพจาก 17.26% ให้ลดลงเหลือ 9.23%

---

# Experiments
- Exp-V: Further Pre-Training on BERT Large
1. จุดประสงค์ในการทดสอบที่ 5 **ทดสอบ การทดลองนี้ได้ลองทดสอบว่าถ้าหากให้ BERT Large ที่มีการใช้ทรัพยากรที่มากยิ่งขึ้นจะส่งผลให้ประสิทธิภาพดีขึ้นหรือไม่ โดยการเปรียบเทียบ ULMFiT ซึ่งเป็น state-of-art สำหรับการทำ Text-Classification กับโมเดล BERT base และBERT large ที่ผ่านการ Fine-Tuning ด้วย task-specific further pre-training ทั้งคู่**

2. ข้อมูลเบื้องต้นเกี่ยวกับ BERT base และ BERT Large
  - BERT-base: 12 layers, 768 hidden units, 12 heads, ~110M parameters in total
  - BERT-large: 24 layers, 1024 hidden units, 16 heads, ~340M parameters in total


---

<img src="Result_BERT_Large.png"/>

<style>
img{
  max-height: 50%;
  margin: 20px auto;
}
</style>

> ผลลัพธ์จะเห็นว่า ULMFiT ที่เป็นโมเดลสำหรับ Text Classification โดยเฉพาะยังไม่สามารถเทียบผลลัพธ์กับ BERT base และ BERT large ได้ แต่ผลลัพธ์ของ BERT large ทำให้ได้ผลลัพธ์ที่ดีที่สุดในชุดข้อมูลทดสอบ แต่ต้องใช้ทรัพยากรในการคำนวณมากกว่า BERT base แน่นอนและใช้ทรัพยากรค่อนข้างสูง รวมถึงเวลาที่ใช้ในการคำนวณ ที่ค่อนข้างมีเวลานาน แต่ถ้ามองจากประสิทธิของโมเดล BERT large อาจมีความจำเป็นสำหรับบางงานที่ต้องการความถูกต้องและผลลัพธ์ออกมาดีที่สุด  

---

 # Conclusion

 งานวิจัยฉบับนี้ทำการทดลอง <font color="salmon">BERT for text classification</font> ในหลากหลายวิธีการที่แตกต่างกัน ซึ่งทุกการทดลองเเสดงให้เห็นถึงข้อดี ข้อเสีย และข้อเปรียบเทียบกับโมเดลอื่น โดยสรุปเป็นใจความสำคัญได้ ดังนี้

  - 1. Layer ชั้น 11 (หรือเรียงจาก input ที่อยู่ขึ้นล่างสุด Layer 0 - Layer11) ของโมเดล BERT เป็นชั้นที่เหมาะกับการทำ Text classification
  - 2. การปรับ Learning rate ให้น้อยลงสามารถแก้ปัญหาที่เกิดขึ้นกับโมเดลได้	
  - 3. การทำ Pre-training model ด้วย within-task และ in-domain ช่วยเพิ่มประสิทธิภาพใน		การทำโมเดล
  - 4. แม้ว่าการทำ Multi-task fine-tunningจะช่วยเพิ่มประสิทธิภาพในการประมวลผลมากกว่า sigle-task <br /> fine-tunning แต่ผลลัพธ์ที่ได้ก็ยังไม่เียบเท่า further pre-traning model
  - 5. BERT สามารถประมวลผลได้ดีแม้ว่าชุดข้อมูลที่นำมาทดสอบจะมีขนาดเล็ก

---