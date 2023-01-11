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

# 训练时冻结参数
```
for name, param in model.named_parameters():
    if "fc1" in name:
        param.requires_grad = False
optimizer = optim.SGD(filter(lambda p : p.requires_grad, model.parameters()),lr=5e-4)
```

# 对bias和layernorm.weight不使用weight_dacay
```
no_decay = ["bias","LayerNorm.weight"]
optimizer_group_parameters = [
    {"params":[p for n, p in model.name_parameters() if not any(nd in n for nd in no_dacay)],
     "weight_decay": training_args.weight_decay,
    },
    {"params":[p for n, p in model.name_parameters() if any(nd in n for nd in no_dacay)],
     "weight_decay": 0.0,},
    ]
optimizer = AdamW(optimizer_grouped_parameters, lr = training_args.learning_rate)
```



# Seed
```
def seed_everything(seed):
    random.seed(seed)
    os.environ['PYTHONHASHSEED'] = str(seed)
    np.random.seed(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)
    torch.backends.cudnn.deterministic = True
    torch.backends.cudnn.benckmark = False

seed_everything(123)
```
model build的过程都与torch有关

固定seed的这个操作最好在所有函数执行之前就先执行了（也就是让 seed_everything(seed）这个函数在程序的最开始执行

如果我们想要每次'默认的都相同'，那就执行两次 seed_everything(seed) 这个函数吧, 设置两个seed。第一次执行，在程序的开头，把所有的torch的seed相关的都固定住，第二次在build model 等之后再执行一次

