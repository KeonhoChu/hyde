---
title: Seoul National University Dental Hospital Challenge
description: 2023 HealthCare AI Competetion SNUDH - [Oral image synthesis data for artificial intelligence learning project]
image: "snudh.png"
date: 2023.12.06 ~ 2023.12.12
---

# 2023 HealthCare AI Competetion SNUDH - [Oral image synthesis data for artificial intelligence learning project] 


## Table of Contents

1. [Breaking Problem](#breaking-problem)
   - [Reproducible Model Performance](#0-reproducible-model-performance)
   - [Imbalanced Train Dataset](#1-imbalanced-train-dataset)
   - [Model Training Speed](#2-model-training-speed)
   - [Hyperparameters](#3-hyperparameters)
   - [Evaluation Dataset (Validation Dataset) Size](#4-evaluation-dataset-validation-dataset-size)
   - [Data Augmentation](#5-data-augmentation)
   - [Saving the Best Performing Model](#6-saving-the-best-performing-model)

2. [Challenge information](#Cahllenge-information)
   - [2023 HealthCare AI Competition SNUDH](#2023-구강이미지-합성데이터-헬스케어-AI-경진대회)
   - [대회주제 (Competition Theme)](#대회주제)
   - [심사 및 평가방식 (Evaluation and Assessment Method)](#심사-및-평가방식)
   - [결과 제출 형식 (Submission Format)](#결과-제출-형식)
   - [시상 및 혜택 (Awards and Benefits)](#시상-및-혜택)
   - [경진대회 일정 (Competition Schedule)](#경진대회-일정)
   - [추진 (Organization)](#추진)

# Breaking Problem
**최종성적 - 3rd ( 우수상 )**

## 0. Reproducible Model Performance
To ensure reproducible model performance, random variable handling has been conducted. All random seeds were fixed to 41.

## 1. Imbalanced Train Dataset
The analysis of the training data revealed an imbalance between the labels. Though Borderline SMOTE was intended for use, due to the absence of the imblearn package in the server setup during the previous virtual environment construction period, simple resampling using the `resampling` function of sklearn was employed to address the label imbalance.

### Original Dataset
- Decayed (1): 17000
- Not Decayed (0): 10000

### Balanced Train Dataset
- Decayed (1): 17000
- Not Decayed (0): 17000

## 2. Model Training Speed

Large scale CNNs (such as ResNet, DenseNet, etc.) guarantee performance given sufficient data, but come with the trade-off of decreased training speed. Analyzing and adjusting oversampling, validation size, hyperparameters, and augmentation methods to conduct model selection within the competition period seemed insufficient. Hence, it was decided to utilize EfficientNet, which is efficient in terms of training speed while maintaining performance.

The two models used (Pretrained = False) are as follows:
- EfficientNet B0
- EfficientNet B3 (approximately twice the size of EfficientNet B0)

### Model Performance
| Model           | Params | f1-score       |
|-----------------|--------|----------------|
| EfficientNet B0 | 5.3M   | 0.98882171429196 |
| EfficientNet B3 | 12M    | 0.9973782689708769 |


## 3. Hyperparameters
- **Batch Size**: A batch size of 32 has been found to be optimal both in terms of training speed and model performance for around 30,000 data points.
- **Learning Rate**: Adam optimizer with an initial learning rate of 3e-4 has been set, as it has shown the most decent performance.
- **Learning Rate Decay Method**: ReduceLROnPlateau scheduler has been used.

## 4. Evaluation Dataset (Validation Dataset) Size
Evaluation data size split from the training data is typically done in ratios like 9:1, 8:2, 7:3. Experimentation with 7:3 and 8:2 ratios revealed better model performance with an 8:2 split.

## 5. Data Augmentation
1) Base (Original Dataset)
2) Random Rotation
3) Random Horizontal Flip
4) Random Vertical Flip
5) Random Augmentation
Although all five methods were attempted and combinations were tested, the base Original Dataset yielded the highest performance. Additionally, Cutmix and Non-rigid transform were desired to be implemented but were hindered due to the absence of the albumentations package in the server setup.

## 6. Saving the Best Performing Model
Continuing training without improvement in performance becomes futile. Hence, early stopping with a patience of 5 epochs has been applied, terminating training if the validation loss does not decrease for 5 consecutive epochs.

## Final Configuration
- Fixed Random Seed
- Oversampling
- EfficientNet B3
- Hyperparameters (Batch Size: 32, Learning Rate: 3e-4, ReduceLROnPlateau, Validation Split: 8:2)
- Base Dataset (No Augmentation)
- Early Stopping



# Challenge information
# 2023 구강이미지 합성데이터 헬스케어 AI 경진대회

구강이미지 합성 데이터 헬스케어 AI경진대회
"2023 NIA 구강이미지 합성데이터셋 구축사업"의 일환으로 추진된 치과 구강이미지 합성 데이터 분야의 헬스케어 AI 경진대회 입니다.
구강이미지 합성데이터를 활용한 충치 치아 분류 AI모델 개발에 도전해보세요!

본 대회는 NAVER CLOUD PLATFORM의 고성능 클라우드 인프라 상에서 진행됩니다.


## 대회주제
구강 이미지 합성 데이터를 활용한 충치 치아를 분류하는 AI 모델 개발

## 심사 및 평가방식
- IT/AI분야 전문가로 구성된 전문 평가위원단 구성 심사 진행
   ① 사전 검토 : 평가 적격/비적격 참여자 선별
   ② 정량 평가 : 평가지표를 통한 점수 산정
- f1-score가 1점에 가까울 수록 높은 점수 부여 (f1-score를 점수로 환산하여 순위 선정)

## 결과 제출 형식
* 프로그램 결과물 및 성능지표
  ① 프로그램 결과물(개발된 모델) : GPU서버 內 정답 디렉토리에 업로드  - 작성된 모델의 소스 파일 (사용한 언어 및 라이브러리의 버전이 작성된 파일)
  ② 성능지표 : GPU서버 內 성능지표 디렉토리에 업로드
* Report (기술문서) 제출
 - 심사 후 수상 대상자 제한 제출  ※ 수상대상 참가자에게는 일정 및 진행사항에 대해 개별 안내드립니다.
 - 결과 및 분석 레포트를 간단히 요약하여 PDF 파일 형태로 제출
 - 레포트에 반드시 포함되어야 하는 내용은 제출팀의 이름, 모형에 대한 간단한 설명
 - 보고서 분량은  A4 1page ~ 10page 이내


## 경진대회 일정
- 참가신청: 2023년 11월 30일(금) ~ 12월 12일(화)
- 대회참가: 2023년 12월 06일(수) ~ 12월 12일(화) 18:00까지


- 심사기간: 2023년 12월 14일(목) ~ 12월 15일(금)
- 결과발표: 2023년 121월 16일(토)
- 시상식: 2023년 12월 21일(수) 예정

## 추진
- 주관: 서울대학교 치과병원
- 후원: 한국지능정보사회진흥원


## 시상 및 혜택
- 총시상팀: 8개팀 / 총상금: 500만원

<table class="tbl_prize">
  <tr>
    <th style="text-align:left;width:50%">시상</th>
    <th style="text-align:center;width:15%">시상 수</th>
        <th style="text-align:left;width:35%">상금</th>
  </tr>
  <tr>
    <td>
      <strong>대상</strong><br>
    </td>
    <td> 1팀 </td>
    <td align=center> 200만원 </td>
  </tr>
 <tr>
    <td>
      <strong>최우수상</strong><br>
    </td>
        <td align=center> 1팀 </td>
       <td style="text-align:center"> 100만원</td>
   </tr>
      <tr>
    <td>
      <strong>우수상</strong><br>
    </td>
        <td align=center> 2팀 </td>
    <td style="text-align:center">각 50만원</td>
   </tr>
   <tr>
    <td>
      <strong>입선</strong><br>
    </td>
        <td align=center> 4팀 </td>
    <td style="text-align:center">각 25만원</td>
   </tr>
</table>










