# 离线安装
将whl文件都放在whl文件夹中
pip install --no-index --find-links=whl -r requirements.txt

# 离线下载
pip wheel -r requirements.txt

# 自动生成requirements.txt
pip install pipreqs
pipreqs /path --encoding=utf8 --force
pip freeze > requirements.txt
