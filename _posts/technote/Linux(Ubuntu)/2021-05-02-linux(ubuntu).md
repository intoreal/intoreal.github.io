---
layout: post
current: post
cover:  assets/images/tag-images/tag-backend.jpg
navigation: True
title: 리눅스(Ubuntu) 자주 사용하는 기능
date: 2021-05-02 12:28:00
tags: [backend]
class: post-template
subclass: 'post tag-backend'
author: intoreal
---

## Linux 환경 점검

### 하드웨어 확인

* CPU 정보

  ```sh
  cat /proc/cpuinfo
  ```

* GPU 정보 1

  ```sh
  lspci | grep -i VGA
  ```

* GPU  정보 2

  ```sh
  nvidia-smi
  ```

  

### 운영체제 확인

-  Linux  커널 버전

  ```
  cat /proc/version
  ```

- Ubuntu 버전

  ```
  cat /etc/issue
  ```

* OS 커널 비트수

  ```sh
  getconf WORD_BIT
  ```

  

### 네트워크 확인

* LISTEN 포트 확인

  ```sh
  netstat -nat | grep LISTEN
  ```

* 외부에서 접근 확인

  ```sh
  python3 -m venv test
  source test/bin/activate
  sudo pip3 install flask
  touch app.py
  vim app.py
  ```
  
  ```python
  # app.py 
  from flask import Flask
  from flask import request
  from flask import redirect
  
  app = Flask(__name__)
  
  @app.route('/', methods = ['GET'])
  def home_get():
      args_dict = request.args.to_dict()
      res = f'Get request arrived! \n{args_dict}'
     	return res
  
  @app.route('/', methods = ['POST'])
  def home_post():
      form_dict = request.form.to_dict()
      file_dict = request.files
      res = f'Post request arrived! \n{form_dict} \nfile num: {len(file_dict)}\n{file_dict}'
     	return res
  
  @app.route('/<path:subpath>', methods = ['GET', 'POST'])
  def home_redirect(subpath):
      return redirect('/')
  
  if __name__== '__main__':
     	app.run(host='0.0.0.0', port=80)
  ```
  
  ``` sh
  sudo python3 app.py
  # 인터넷 환경에서 서버 IP:80으로 접근 시도
  ```
  
  

## tmux 사용

* tmux 세션 생성

  ```sh
  tmux new -s <session-name>
  ```

* tmux 세션에서 나오기

  ```sh
  Ctrl+b, d
  ```

* tmux 세션 리스트 확인

  ```sh
  tmux ls
  ```

* tmux 세션 들어가기

  ```sh
  tmux attach -t <session-name>
  ```

  