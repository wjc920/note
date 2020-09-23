# 文件压缩和解压

## zip
 
``` sh
# /home/html下所有文件文件夹打包到html.zip
# 包含html文件夹
zip -q -r html.zip /home/html

# 不含html文件夹
zip -q -r html.zip *

# 删除zip中的a.c
zip -dv html.zip a.c
```