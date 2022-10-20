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
f.clode()

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
