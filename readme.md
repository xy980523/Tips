# txt文档

### 读取：
```
data = open('a.txt','r', encoding='utf-8').readlines() 
for i in range(len(data)):  
    line = data[i].strip().split(' ')  
    a = line[0]  
    b = line[1]  
```
  
  
