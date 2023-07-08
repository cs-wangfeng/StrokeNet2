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

### 调研
关于韩语字母的频率，有一个[中文链接](https://m.hujiang.com/kr/p195931/)    
图片：  
<img src="https://github.com/cs-wangfeng/StrokeNet2/assets/83827774/220fabea-2c08-4ba4-adbc-649988837b37" style="zoom:25%;" />


有些细节需要明白：    
- ㅐ是分成哪两部分（两种切分方式）  
- ㅝ的右侧部分算是ㅓ吗    
搜索到[韩国网站](https://www.korean.go.kr/hangeul/principle/001.html)，比较有帮助    

字母拆分：    
<img src="https://github.com/cs-wangfeng/StrokeNet2/assets/83827774/8ed72772-1a78-42e9-b3b4-4fcbc4afa4b6" style="zoom:25%;" />

### 得到24基本韩语字母排序以及对应的英文字母：  
*：通过韩国科学技术院统计的40字母出现频率经过拆分和计算得到24基本字母频率  
| 韩语字母 | 英文字母 | * |       *     |      *      |       *     |    *        |     *       |       *     |        *    |      *      |       *     | 总频率        |
|------|------|----------------------------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|
| ㅇ    | e    | 0.12685701                       |            |            |            |            |            |            |            |            |            | 0.12685701 |
| ㅣ    | t    | 0.01961272                       | 0.0008038  | 0.01760322 | 0.00208988 | 0.00052247 | 0.00498356 | 0.00008038 | 0.00221045 | 0.00876142 | 0.06165146 | 0.11831936 |
| ㅏ    | a    | 0.08500185                       | 0.01961272 | 0.00815857 | 0.00052247 |            |            |            |            |            |            | 0.11329561 |
| ㄴ    | o    | 0.08875804                       |            |            |            |            |            |            |            |            |            | 0.08875804 |
| ㄱ    | i    | 0.07446345                       | 0.00502404 |            |            |            |            |            |            |            |            | 0.07948749 |
| ㄹ    | n    | 0.0628005                        |            |            |            |            |            |            |            |            |            | 0.0628005  |
| ㅅ    | s    | 0.04156795                       | 0.0209335  |            |            |            |            |            |            |            |            | 0.06250145 |
| ㅓ    | h    | 0.0409938                        | 0.01760322 | 0.00305444 | 0.00008038 |            |            |            |            |            |            | 0.06173184 |
| ㅡ    | r    | 0.05039826                       | 0.00876142 |            |            |            |            |            |            |            |            | 0.05915968 |
| ㅗ    | d    | 0.03942639                       | 0.00815857 | 0.00052247 | 0.00498356 |            |            |            |            |            |            | 0.05309099 |
| ㄷ    | l    | 0.03815878                       | 0.00550252 |            |            |            |            |            |            |            |            | 0.0436613  |
| ㅈ    | c    | 0.03642429                       | 0.00143544 |            |            |            |            |            |            |            |            | 0.03785973 |
| ㅜ    | u    | 0.02821338                       | 0.00305444 | 0.00008038 | 0.00221045 |            |            |            |            |            |            | 0.03355865 |
| ㅎ    | m    | 0.03223759                       |            |            |            |            |            |            |            |            |            | 0.03223759 |
| ㅁ    | w    | 0.03014424                       |            |            |            |            |            |            |            |            |            | 0.03014424 |
| ㅂ    | f    | 0.02523982                       | 0.0011962  |            |            |            |            |            |            |            |            | 0.02643602 |
| ㅕ    | g    | 0.0196931                        | 0.00208988 |            |            |            |            |            |            |            |            | 0.02178298 |
| ㅊ    | y    | 0.01034713                       |            |            |            |            |            |            |            |            |            | 0.01034713 |
| ㅌ    | p    | 0.00622024                       |            |            |            |            |            |            |            |            |            | 0.00622024 |
| ㅍ    | b    | 0.00550252                       |            |            |            |            |            |            |            |            |            | 0.00550252 |
| ㅛ    | v    | 0.004019                         |            |            |            |            |            |            |            |            |            | 0.004019   |
| ㅑ    | k    | 0.00269273                       | 0.0008038  |            |            |            |            |            |            |            |            | 0.00349653 |
| ㅠ    | j    | 0.00269273                       |            |            |            |            |            |            |            |            |            | 0.00269273 |
| ㅋ    | x    | 0.00233259                       |            |            |            |            |            |            |            |            |            | 0.00233259 |


### 接下来构造ko2letter.txt表（类似vocab/zh2letter.txt）  

首先获得韩语的文字表[链接](https://www.loc.gov/marc/specifications/specchareacc/KoreanHangul.html)

通过处理得到korean_char.txt，共2028行  

调研得到hgtk(python lib)可以用于拆分韩文字

使用decompose.py将korean_char.txt通过字母拆解编号的方式得到每个韩文字对应的拉丁字母化结果

删去ancient korean等一些无法显示的韩语文字，获得最终版的ko2letter.txt表

经检查发现，hgtk对于韩文字的拆分并不彻底，例如‘없’拆完之后最小单元仍包含‘ㅄ’，这样的拆分不彻底的情况完全发生于韩文字下部含有两个基本字母的情况，编写代码查询有多少个这样的情况，因为这种情况下未拆分彻底的内容不会显示，会与其他韩文字发生重复，因此查询重复的拆分拉丁字母序列即可，查询代码见find_same.py。  

经过查询，有49种情况重复，只有一种情况是韩文字重复，其余全是由于拆分不彻底导致的。（修改前后重复结果见find_same.txt和find_same1.txt，find_same1.txt的那个就是韩文字重复的情况）  

添加的新的匹配内容（修改内容）如下：   
```python
elif letter == 'ㅀ':
            letter_list.append('nm')
        elif letter == 'ㄺ':
            letter_list.append('ni')
        elif letter == 'ㄼ':
            letter_list.append('nf') 
        elif letter == 'ㄿ':
            letter_list.append('nb')
        elif letter == 'ㄾ':
            letter_list.append('np')
        elif letter == 'ㄻ':
            letter_list.append('nw')                      
        elif letter == 'ㅄ':
            letter_list.append('fs')
        elif letter == 'ㄽ':
            letter_list.append('ns')
        elif letter == 'ㄶ':
            letter_list.append('om')
        elif letter == 'ㄳ':
            letter_list.append('is')
        elif letter == 'ㄵ':
            letter_list.append('oc')
```

至此：
ori_ko_char.txt为原2028韩文字表   
ori_ko2letter.txt为原2028韩文字对应拉丁字母表  
ko2letter.txt为删减（ancient Hangul）过后的韩文字对应拉丁字母表  


