# torch.cuda模块获取信息

## 判断GPU是否可用

```python
import torch 
print(torch.cuda.is_available())
```

如果输出True则表示可以使用GPU

## 输出可使用GPU的数量

```python
import torch
print(torch.cuda.device_count())
```

输出1就表示只有一块可以用

## 输出GPU的名字

```python
import torch
print(torch.cuda.get_device_name())
```

如果有多块，就写一个循环

```python
import torch
for i in range(torch.cuda.device_count()):
    print(f"Device{i}: {torch.cuda.get_device_name(i)}")
```

## 完成的程序

```python
import torch

if torch.cuda.is_available():
    print("CUDA is available")
    # the number of GPU
    print(f"CUDA device count: {torch.cuda.device_count()}")
    for i in range(torch.cuda.device_count()):
        device = torch.device(f'cuda:{i}') # cuda是一种type, cuda:0就表示第一块GPU，可以作为变量
        print(f'-----Device{i}-----')
        # the name of device
        print(f"Name: {torch.cuda.get_device_name(device)}")
        # the capability of device
        print(f"Capability: {torch.cuda.get_device_capability(device)}")
        # the memories of device
        print(f"Total Memories(GB): {torch.cuda.get_device_properties(device).total_memory/1024**3}")
else:
    print("CUDA is not available")
```



这时候`i`设置的是0

![image-20230530195441705](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230530195441705.png)



GPU的数量最多是128块, index到127, 不然就溢出了

![image-20230530195923695](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230530195923695.png)

## 查看cuda算力