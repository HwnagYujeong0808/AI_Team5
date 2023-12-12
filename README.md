# AI_Team5
This is a GitHub repository for a team project in an Artificial Intelligence class.

Team members: 20102128 Yujung Hwang, 17102063 Yooseok Lee, 17102047 Jihoon Moon

> **Google Drive containing all our code files, datasets, and models**: https://drive.google.com/drive/folders/15xNLqFqYo6bK5Jg3ehTNBYbANsL_2Cu8?usp=drive_link


## Motivation for the project and an explanation of the problem statement
> Motivation for the project

With the recent advancement of online video services and social media, there is a growing demand for 'short-form content' that can be consumed in a brief period.

![image](https://github.com/HwnagYujeong0808/AI_Team5/assets/66208800/5131ec68-85ee-438f-a1a5-971227d6ad88)

Table 1, displaying the results of a survey conducted on 5,000 individuals aged 15 to 59 in South Korea, illustrates the increase in the usage of short-form content over the past year. As indicated in Table 1, the number of users who watched short-form content has increased by more than 10% in the last year.


> Problem Definition

In today's society, where a large amount of information is generated and shared, content consumers have become accustomed to videos that are less than one minute long. There is a tendency to skip through long videos without watching them to the end and move on to the next one.
From the perspective of video content creators, manually editing long videos which are the source of short-form content, to extract highlight is highly inefficient and demands a significant amount of time and resources.


## A description of the data

- **Data 1: ETRI Korean Emotion Dataset - KEMDy20 (General Public Free Speech) Dataset**

  - **Link**: [KEMDy20\_Dataset](https://nanum.etri.re.kr/share/kjnoh/KEMDy20?lang=ko_KR)
  - **Introduction**: A multimodal emotion dataset collected for the analysis of the correlation between emotional speech, contextual meaning of speech, and physiological response signals such as skin conductance, heart rate-related data, and wrist skin temperature.
  - **Train set**
    - Download path: '01.데이터/2.Validation/원천데이터/VS\_유튜브\_04'
    - Only the video data within the smallest 21.4GB folder is used.
  - **Test set**
    - Download path: '01.데이터/2.Validation/원천데이터/VS\_유튜브\_01'
    - Only 8 video data within the folder are used
      - '유튜브*기타\_19843', '유튜브*반려동물및동물*2153', '유튜브*스타일링및뷰티*14630', '유튜브*스포츠*4174', '유튜브*여행*7640', '유튜브*음식*17341', '유튜브*일상*10479', '유튜브*자동차\_0094'

- **Data 2: AI HUB Video Content Highlight Editing and Description (Summarization) Data**
  - **Link**: [AIHUB\_Dataset](https://www.aihub.or.kr/aihubdata/data/view.do?dataSetSn=616)
  - **Information**: The AI HUB dataset on video content highlight editing and description (summarization) is a training dataset constructed by labeling the positions of key scenes in news and YouTube videos and tagging them for category items

## Model Hyperparameter and architecture choices that were explored

> Model hyperparameters

+ **learning_rate**: The step size at each iteration while moving toward a minimum of a loss function. In this case, it was set to 0.001.

+ **epochs**: The number of complete passes through the training dataset. it was set to 100.

+ **input_size**: The number of expected features in the input x. It was 32 for this model.

+ **hidden_size**: The number of features in the hidden state h. It was set to 128.

+ **output_size**: The number of features in the output y, or the size of the output layer. For this model, it was 7, which often corresponds to the number of classes in a classification task.

+ **num_layers**: The number of recurrent layers (e.g., number of stacked LSTMs). Here, there are 3 layers.

+ **kernel_size**: The size of the convolving kernel for a convolutional neural network (CNN). It was set to 3.

+ **num_channels**: The number of channels produced by the convolution, essentially the number of output filters in the convolution. It was 16 in this model.

+ **stride**: The stride of the convolution. It was set to 1, which means the filter moves one pixel at a time during the convolution.

> Model architecture

![image](https://github.com/HwnagYujeong0808/AI_Team5/assets/66208800/9d4490a1-ce43-4353-8476-01dccbbe76d4)

**STEP 1**
- Using the ETRI dataset to train a audio Emotion classification model.
- Emotion Classification model Type : LSTM, 1D CNN, LSTM with Attention, GRU

**STEP 2**
- The MFCC extracted from the voice in the AI Hub YouTube video was then combined with the output tensors inferred by the three trained models into a single vector

**STEP 3**
- For video image feature extraction, pre-trained ViT models are used to perform feature exraction on an image frame-by-frame basis

**STEP 4**
- Finally **LSTM-based Multimodal Highlight Detection Model
using Video and Audio Emotional Information** combines feature
vectors extracted from audio and video to detect highlights in every
second frame of the video.


## Presentation of results
> Training loss curve of four audio emotion classification model

+ 1) LSTM, 2. 1D CNN, 3. LSTM with Attention, and 4. GRU

![image](https://github.com/HwnagYujeong0808/AI_Team5/assets/66208800/a9dd68a6-868d-4f63-bf7f-2a91c70ae854)

> Video highlight classification model

+ The graph above shows the result of highlighting using only audio, and the graph below shows the result of highlighting using video and audio.
+ 1. LSTM, 2. 1D CNN, 3. LSTM with Attention, and 4. GRU

![image](https://github.com/HwnagYujeong0808/AI_Team5/assets/66208800/40b37feb-2b60-41e1-b7e8-6cb85f20c77e)

+ From left, Audio highlight extraction model, Multimodal highlight extraction 
  
## Analysis of results

- Compared to audio-only highlight extraction, the difference in performance graphs between RNNs and CNNs is almost eliminated, and there is a modest increase in accuracy. In particular, for LSTM and GRU with Attention, the threshold for reversing the f1 score based on precision is higher than for LSTM alone. This may not be a direct result of applying images, but it may be due to the structure of capturing long-term dependencies.

## Any insights and discussions relevant to the project
- Since we have learned LSTM, CNN, Attention mechanism, and GRU, we have used deep learning model LSTM, CNN, LSTM with attention, and GRU to classify the emotion an input of audio highlight extraction. However, using Wav2Vec 2.0, a state-of-the-art method, would show a better performance. It is a speech representation model developed by Facebook AI Research (FAIR). It is designed for unsupervised pre-training of speech representations, which can later be fine-tuned for various downstream speech-related tasks such as automatic speech recognition (ASR) and speaker identification.

![image](https://github.com/HwnagYujeong0808/AI_Team5/assets/66208800/a225a6a5-aea2-44cf-9a3a-9b855cc8829f)


## References
+ F. Qi, X. Yang and C. Xu, "Emotion Knowledge Driven Video Highlight Detection," in IEEE Transactions on Multimedia, vol. 23, pp. 3999-4013, 2021.


## Extra credit
### Member's contribution statement

+ **Yujung Hwang**
  + Developed audio highlight classification models.
  + Fine-tuned video highlight classification models.

+ **Yooseok Lee**
  + Led the multimodal model development.
  + Designed the model architecture.

+ **Jihoon Moon**
  + Built four audio emotion classification models.
  + Documented and explained the project code.
