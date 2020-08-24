# 点击选择文字验证码识别
文字点选、选字、选择文字验证码识别  
![Image text](./doc/fc2b0.png)    
**特点**  
纯pytorch实现，无需安装其他复杂依赖  
单个模型在50M左右，总共加起来134M,且有进一步缩小的空间  
单次识别速度约在200~300ms之间，使用GPU话会更快
## 免责声明
**该项目仅用于技术交流，不得在任何商业使用！**
## 实现逻辑
使用了约3000张左右的验证码进行训练，通过率达到95%以上
偶尔有些文字识别错了也没关系，依然能通过  
**识别逻辑**  
1、利用yolo框选出给出的文字和图中出现的文字，作为题目  
2、利用crnn识别给定的文字，作为答题范围  
3、根据答题范围，利用cnn预测图片中出现的文字是那个  

**模型文件**  
模型文件在model目录下  
卷积神经网络模型 cnn_iter.pth（用于识别图片中的文字）  
卷积神经网络+CTCloss模型 ocr-lstm.pth（用于识别标题中的文字）   
yoloV3模型 yolov3_ckpt.pth （用于框选出图片中的文字和标题）    
**模型结构**  
模型结构存放在src/utils中

## 环境准备
1、安装python3.6（建议使用anconda）  
2、建立虚拟环境  
3、pip install -r requirements.txt
## 如何使用

```python demo.py```  
结果如下  
```json
[
    {
        "crop": [
            231,
            173,
            297,
            248
        ],
        "classes": "target",
        "content": "拌"
    },
    {
        "crop": [
            0,
            344,
            114,
            385
        ],
        "classes": "title",
        "content": "凉拌牛肚"
    },
    {
        "crop": [
            58,
            189,
            125,
            265
        ],
        "classes": "target",
        "content": "牛"
    },
    {
        "crop": [
            231,
            271,
            297,
            343
        ],
        "classes": "target",
        "content": "肚"
    },
    {
        "crop": [
            201,
            79,
            265,
            152
        ],
        "classes": "target",
        "content": "凉"
    }
]
```
![Image text](./doc/123.jpg)  
## 效果演示
**以bilbil登录验证码为例**  
```python bilbil.py```  
![Image text](./doc/bilibili_1.gif)  
![Image text](./doc/bilibili_2.gif)  




# 参考资料
https://github.com/ypwhs/captcha_break  
https://github.com/eriklindernoren/PyTorch-YOLOv3  
https://github.com/meijieru/crnn.pytorch  
https://github.com/chineseocr/chineseocr  
https://github.com/JiageWang/hand-writing-recognition

### 点个**star**再走呗！ 