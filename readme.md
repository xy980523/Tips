# txt文档

### 读取
```
data = open('a.txt','r', encoding='utf-8').readlines() 
for i in range(len(data)):  
    line = data[i].strip().split(' ')  
    a = line[0]  
    b = line[1]  
```

### 写入
```
f = open('a.txt','w')
f.write('...' + '\n')
f.close()

```
  
# csv文件

### 读取
```
import csv
csvreader = csv.reader(open('a.csv','r'))
csv_list = list(csvreader)
for i in range(len(csv_list)):
    print(csv_list[i][0])
```

### 写入
```
import csv

f = open('a.csv', 'w', encoding='utf-8', newline='' "") 
csv_writer = csv.writer(f)
csv_writer.writerow(['A','B','C','D'])
for i in range(5):
    csv_writer.writerow(['a','b','c','d'])
f.close()
```
# checkpoint

### 读取
```
ckpt = torch.load('ResNet_pt/resnet18-5c106cde.pth')
如果是读取用pytorch或者pytorch_lightning训练得到的模型：
ckpt = torch.load('ResNet_pt/resnet18-5c106cde.pth')['state_dict']

然后
model.load_state_dict(ckpt,strict=False)
或者
model.load_state_dict({k.replace('module.',''):v for k,v in ckpt.items()})
model.load_state_dict({k.replace('model.',''):v for k,v in ckpt.items()})

```

# 字典

### 新建字典

```
srs = {}
files = glob.glob('*.wav')
for file in files:
    wav, sr = torchaudio.load(file)
    if sr in srs:
        srs[sr] +=1
    else:
        srs[sr] = 1
```
