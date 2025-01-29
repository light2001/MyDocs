### Introduce
The purpose of writing this article is to run a large model on a laptop computer, similar to the effect of achieving online AI, such as Doubao, Baidu Wenxin Word and other     AI tools

The installation part of this article is only suitable for beginners with less foundation, and the master can ignore this link.

For reasons you all know, many of the actions in this article require a ladder to navigate.
<br>
<br>
<br>
#### Required software

Below is a list of the required sofware
- python
  - pip
- ollama
- open-webui



##### Python

The python environment is used to run the open-webui of the client, which can be used instead of the ollama terminal
pip is the package manager needed to install python




<br>
<br>
<br>
##### Ollama

Ollama is a large model management platform that provides everything you need to download and run large models.
  
It only takes very simple steps to run large models on the computer



##### Open-webui

 Usually, after you install ollama, you run the model and can only type text in the terminal, which is not too convenient to use, so you need an interface similar to other web version of AI tools, here it is recommended to use the open-webui program written in python
    



#### Destination

The goal of this article is to run deepseek's r1 1.5b model on a laptop, but it also applies to other models included on the ollama platform

<br>
<br>
<br>

### Installation

This section explains how to install the required software
Since I only have windows at hand, here is how to install windows

#### Python & pip

##### Install python
Go to the official python [website](https://www.python.org/) to download the installation package, and select this version here:

Click Download to install
![image](https://github.com/user-attachments/assets/164a0620-be6e-42ca-bbac-82a641c7a5a2)

![image](https://github.com/user-attachments/assets/5bfb6ac7-38cb-4240-8061-ef7cd9d6c2d2)

The installation method is a point-and-click next and the next step is fine.

Input below command
~~~
python
~~~
If you see below screenshot, the python install is completed.
![image](https://github.com/user-attachments/assets/08ba7115-64f9-412b-a8c3-f5bfbd3ba203)


##### Install pip

For windows users, you just need to set the environment variable and pip is installed.

<br>
<br>
Follow the steps in the screenshot below to set the environment variables
![image](https://github.com/user-attachments/assets/8f3518d2-9c28-4f32-8923-5c67d04e81b5)
![image](https://github.com/user-attachments/assets/e6760b9e-596d-454e-a065-01bf2fb58ec1)

![image](https://github.com/user-attachments/assets/843fe858-100a-4a87-a077-f974dcbabe27)

![image](https://github.com/user-attachments/assets/5b2bff7a-170f-41d8-9567-2e96705aedaf)

Below is the environment variables for Python and PIP 
![image](https://github.com/user-attachments/assets/63512781-3cc1-4f1b-8a92-c302caaf1044)

Input below command 
~~~
pip --version
~~~
If you see below screenshot, the pip install is completed.
![image](https://github.com/user-attachments/assets/6e713f85-c06c-45c4-bf02-b51ff6680307)





##### Mirror image
What is a mirror image?<br>
For some reason, foreign websites cannot be accessed in the country, so you need to set up a domestic mirror site, otherwise pip will not work properly

<br>
The following uses [Tsinghua](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/) Source as an example to set an image
Input the follwing command
~~~
pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
~~~


#### Ollama
Open ollama making address: [https://github.com/ollama/ollama](https://github.com/ollama/ollama)
Find the Release section on the right and click to select the latest release
![image](https://github.com/user-attachments/assets/03f297a3-77e2-4a63-ac1d-dfd056117023)

Select the version below on the page that opens
![image](https://github.com/user-attachments/assets/663029a0-2f4e-4161-97f4-fce5cfd857b8)

##### Environment variable

Environment variables have been described above, here will not repeat, as shown in the screenshot below to set the environment variable is good
![image](https://github.com/user-attachments/assets/2bb7a82c-5164-4332-96a7-2ea773e3f75b)


#### Open-webui

This step depends on pip, so the python link above is a must.

Input below command to install open-web-ui
~~~
pip install open-webui
~~~


<br>
<br>
<br>
### Run large model

#### Server
Input below command.
~~~
ollama serve
~~~
You will see below command line.
![image](https://github.com/user-attachments/assets/4ad72c40-a858-4456-8a2c-5f8bd107e786)


#### Client
Input below command.
~~~
  ollama run deepseek-r1:1.5b
~~~
The first run of this command will perform the download and install steps, if it is already installed, the second run will not have it and will run the model directly
![image](https://github.com/user-attachments/assets/6e89bac0-8499-42a2-a21e-6697eef47a01)


#### Web Client
Input below command.
~~~
open-webui serve
~~~

The first run will download the front and back end and run, the second run will not download the step, will run directly
![image](https://github.com/user-attachments/assets/7e52566b-fa7a-4c45-b1f6-c42f3fb16cf8)

The first login will require an administrator account and password, as shown in the screenshot below
![image](https://github.com/user-attachments/assets/1e08607a-17b1-491c-85b9-00ecef900519)

Here you can select all models locally
![image](https://github.com/user-attachments/assets/e36e1b9d-c9de-4a7b-9d48-10b0cd96c9a9)

Then you can have fun with the big models

### Other Big Model
Open [Ollama's official site](https://ollama.com/), you can see all the big models they have included, and you can choose which ones you want
![image](https://github.com/user-attachments/assets/f5d664da-5f1e-4811-ba06-03b5061e68ad)

Here is the running command.
![Uploading image.png…]()



### Reference
- [How to install ollama](https://ollama.readthedocs.io/quickstart/)
