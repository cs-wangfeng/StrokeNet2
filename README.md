# StrokeNet2
Expanding the StrokeNet paper

## 数据获取
使用`iwslt2017`的数据集，huggingface的[公开数据集链接](https://huggingface.co/datasets/iwslt2017/tree/refs%2Fconvert%2Fparquet/iwslt2017-ko-en)在此  

[此数据集Ko-En部分的有关论文](https://pdfs.semanticscholar.org/00a4/354239b78d5ca46ca705dd0cbf0c589025fa.pdf)，之后可能参考作为baseline；

以及有关这个数据集的[论文](https://aclanthology.org/2017.iwslt-1.1.pdf)  

## 数据清洗
使用change.py将parquet类型文件转换为txt文件（需要修改文件名称如train, validation, test等）

使用split.py将原有包含韩语和英语的txt文件分成两个文件，分别包含韩语和英语（需要修改文件名称如train, validation, test等）

## 韩语字母拉丁化
关于韩语字母的频率，有一个[中文链接](https://m.hujiang.com/kr/p195931/)

有些细节需要明白：  
- ㅐ是分成哪两部分（两种切分方式）
- ㅝ的右侧部分算是ㅓ吗

