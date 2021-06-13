---
layout: post
current: post
cover:  assets/images/tag-images/tag-ai.jpg
navigation: True
title: Tensorflow 기본 문법
date: 2021-04-25 22:59:00
tags: [ai, tensorflow]
class: post-template
subclass: 'post tag-ai'
author: intoreal
---

## 모델 저장
```python
modelpath = '/content/drive/My Drive/Colab/main/'
modelname = 'model'
saver = tf.train.Saver()
saver.save(sess, modelpath+modelname)
```

## 모델 복구 1
```python
modelpath = '/content/drive/My Drive/Colab/main/'
modelname = 'model'
if tf.train.checkpoint_exists(modelpath+modelname):
  saver.restore(sess, modelpath+modelname)
  print('Model Restored!')
else:
  sess.run(tf.global_variables_initializer())
  print('Model Initialized(reset)!')
```

## 모델 복구 2
```python
ckpt = tf.train.get_checkpoint_state('./저장경로/')
if ckpt and tf.train.checkpoint_exists(ckpt.model_checkpoint_path):
  saver.restore(sess, ckpt.model_checkpoint_path)
  print('Model Restored!')
else:
  sess.run(tf.global_variables_initializer())
  print('Model Initialized(reset)!')
```