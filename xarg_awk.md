# xarg & awk

## tips

### 0. 行转列

* case 1
> 有一个敏感词文件，内容格式是"a","b","c"，希望把内容转换为列，并且去除逗号，和双引号“”

 * 方案一
```bash
gosber@freedamadeMacBook-Pro  ~  awk -F',' -v OFS="\n" '{$1=$1;print }' 敏感词.csv
"偏方"
"發票代開"
"发票代开"
"制作文凭"
"神奇面霜"
"神皂"
```

 * 方案二
```bash
gosber@freedamadeMacBook-Pro  ~  xargs -n1 < 敏感词.csv  > m1.txt

gosber@freedamadeMacBook-Pro  ~  cat m1.txt
偏方,發票代開,发票代开,制作文凭,神奇面霜,神皂,中华神水...

gosber@freedamadeMacBook-Pro  ~  awk 1 RS=",|\n"  <m1.txt > 敏感词2.csv
gosber@freedamadeMacBook-Pro  ~  head 敏感词2.csv
偏方
發票代開
发票代开
制作文凭
神奇面霜
神皂
中华神水
印度神油
占卜
巫毒娃娃
```
