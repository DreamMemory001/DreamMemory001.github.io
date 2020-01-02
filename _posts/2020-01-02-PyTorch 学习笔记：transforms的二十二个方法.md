---
layout:     post
title:      PyTorch 学习笔记
subtitle:   transforms的二十二个方法
date:       2020-01-02
author:     TkiChus
header-img: img/post-bg-openmv.jpg
catalog: true
tags:
    - TkiChus
    - DreamMemory001 Blog
    - PyTorch
---

# PyTorch 学习笔记：transforms的二十二个方法
##  一、裁剪-Crop
### 1.随机裁剪：transforms.RandomCrop
class torchvision.transforms.RandomCrop(size, padding=None, pad_if_needed=False, fill=0, padding_mode=‘constant’)
功能：依据给定的size随机裁剪

参数：size- (sequence or int)，若为sequence,则为(h,w)，若为int，则(size,size)  

padding-(sequence or int, optional)，此参数是设置填充多少个pixel。

当为int时，图像上下左右均填充int个，例如padding=4，则上下左右均填充4个pixel，若为3232，则会变成4040。

当为sequence时，若有2个数，则第一个数表示左右扩充多少，第二个数表示上下的。当有4个数时，则为左，上，右，下。

fill- (int or tuple) 填充的值是什么（仅当填充模式为constant时有用）。int时，各通道均填充该值，当长度为3的tuple时，表示RGB通道需要填充的值。

padding_mode- 填充模式，这里提供了4种填充模式，1.constant，常量。2.edge 按照图片边缘的像素值来填充。3.reflect，暂不了解。 4. symmetric，暂不了解。

### 2.中心裁剪： transforms.CenterCrop

class torchvision.transforms.CenterCrop(size)  

功能：依据给定的size从中心裁剪  参数：  size- (sequence or int)，若为sequence,则为(h,w)，若为int，则(size,size)

### 3. 随机长宽比剪裁 transforms.RandomResizedCrop

class torchvision.transforms.RandomResizedCrop(size, scale=(0.08, 1.0), ratio=(0.75, 1.3333333333333333), interpolation=2)

功能：随机大小，随机长宽比裁剪原始图片，最后将图片resize到设定好的size

参数：
size- 输出的分辨率

scale- 随机crop的大小区间，如scale=(0.08, 1.0)，表示随机crop出来的图片会在的0.08倍至1倍之间。
ratio- 随机长宽比设置

interpolation- 插值的方法，默认为双线性插值(PIL.Image.BILINEAR)

### 4. 上下左右中心裁剪： transforms.FiveCrop

class torchvision.transforms.FiveCrop(size)
功能：对图片进行上下左右以及中心裁剪，获得5张图片，返回一个4D-tensor

参数：
size- (sequence or int)，若为sequence,则为(h,w)，若为int，则(size,size)

### 5. 上下左右中心裁剪后翻转： transforms.TenCrop

class torchvision.transforms.TenCrop(size, vertical_flip=False)

功能：对图片进行上下左右以及中心裁剪，然后全部翻转（水平或者垂直），获得10张图片，返回一个4D-tensor。

参数：
size- (sequence or int)，若为sequence,则为(h,w)，若为int，则(size,size)
vertical_flip (bool) - 是否垂直翻转，默认为flase，即默认为水平翻转

## 二、翻转和旋转 ---Flip and Rotation

### 6.依概率p水平翻转 transforms.RandomHorizontalFlip

class torchvision.transforms.RandomHorizontalFlip(p=0.5)

 功能：依据概率p对PIL图片进行水平翻转  

 参数：

 p- 概率，默认值为0.5

### 7.依概率p垂直旋转transforms.RandomVerticalFlip

class torchvision.transforms.RandomVerticalFlip(p=0.5)  

功能：依据概率p对PIL图片进行垂直翻转  

参数：  

p- 概率，默认值为0.5

### 8.随机旋转： transforms.RandomRotation

class torchvision.transforms.RandomRotation(degrees, resample=False, expand=False, center=None)
功能：依degrees随机旋转一定角度

参数：

degress- (sequence or float or int) ，若为单个数，如 30，则表示在（-30，+30）之间随机旋转
若为sequence，如(30，60)，则表示在30-60度之间随机旋转

resample- 重采样方法选择，可选 PIL.Image.NEAREST, PIL.Image.BILINEAR, PIL.Image.BICUBIC，默认为最近邻

expand- ?
center- 可选为中心旋转还是左上角旋转

## 三、图像变换

### 9. resize： transforms.Resize

class torchvision.transforms.Resize(size, interpolation=2)
功能：重置图像分辨率

参数：

size- If size is an int, if height > width, then image will be rescaled to (size * height / width, size)，所以建议size设定为h*w

interpolation- 插值方法选择，默认为PIL.Image.BILINEAR

### 10. 标准化： transforms.Normalize

class torchvision.transforms.Normalize(mean, std)  

功能：对数据按通道进行标准化，即先减均值，再除以标准差，注意是 h*w*c

### 11.转为tensor：transforms.ToTensor

class torchvision.transforms.ToTensor

 功能：将PIL Image或者 ndarray 转换为tensor，并且归一化至[0-1]

 注意事项：归一化至[0-1]是直接除以255，若自己的ndarray数据尺度有变化，则需要自行修改。

### 12.填充：transforms.Pad

class torchvision.transforms.Pad(padding, fill=0, padding_mode=‘constant’)
功能：对图像进行填充

参数：

padding-(sequence or int, optional)，此参数是设置填充多少个pixel。
当为int时，图像上下左右均填充int个，例如padding=4，则上下左右均填充4个pixel，若为3232，则会变成4040。

当为sequence时，若有2个数，则第一个数表示左右扩充多少，第二个数表示上下的。当有4个数时，则为左，上，右，下。

fill- (int or tuple) 填充的值是什么（仅当填充模式为constant时有用）。int时，各通道均填充该值，当长度为3的tuple时，表示RGB通道需要填充的值。

padding_mode- 填充模式，这里提供了4种填充模式，1.constant，常量。2.edge 按照图片边缘的像素值来填充。3.reflect，？ 4. symmetric，？

### 14.转灰度图：transforms.ColorJitter

class torchvision.transforms.ColorJitter(brightness=0, contrast=0, saturation=0, hue=0)  

功能：修改修改亮度、对比度和饱和度

### 15.线性转换：transforms.LinearTransformation（）

class torchvision.transforms.LinearTransformation(transformation_matrix)
功能：对矩阵做线性变化，可用于白化处理！ whitening: zero-center the data, compute the data covariance matrix

参数：

transformation_matrix (Tensor) – tensor [D x D], D = C x H x W

### 16.仿射变换：transforms.RandomAffine

class torchvision.transforms.RandomAffine(degrees, translate=None, scale=None, shear=None, resample=False, fillcolor=0)  

功能：仿射变换

### 17. 依概率p转为灰度图：transforms.RandomGraycale

class torchvision.transforms.RandomGrayscale(p=0.1)  

功能：依概率p将图片转换为灰度图，若通道数为3，则3 channel with r == g == b

### 18.将数据转换为PILImage：transforms.ToPILImage

class torchvision.transforms.ToPILImage(mode=None)
功能：将tensor 或者 ndarray的数据转换为 PIL Image 类型数据

参数：

mode- 为None时，为1通道， mode=3通道默认转换为RGB，4通道默认转换为RGBA

## 四、对transforms操作，使数据增强更加灵活

> PyTorch不仅可设置对图片的操作，还可以对这些操作进行随机选择，组合

### 19. transforms.RandomChoice（transforms）

功能：从给定的一系列transforms中选一个进行操作，randomly picked from a list

### 20.transforms.RandomApply（transforms， p=0.5）

功能：给一个transform加上概率，以一定的概率执行该操作

### 21.transforms.RandomOrder

功能：将transforms中的操作顺序随机打乱

### 22.transforms.Compose（[]）

功能：一般用Compose把多个步骤组合起来
