# ZH-EN Parallel Wikipedia Biography Article Corpus
We compiled a small parallel ZH-EN Wikipedia Biography article corpus with preserved document structure (i.e. section boundaries and headings). This corpus is also used in our research on [Strucutred Document Neural Machine Translation](https://github.com/JZ95/Exploiting-Document-Substructure-in-Neural-MT).

## Preprocessing Workflow
The documents in this corpus are strict translations, NOT comparable articles (i.e., wiki biographies dececribing the same person but written independently). The data is from wikidump, we used the `zhwiki` and `enwiki` dump progress on `20190329`, which might be unavailable right now. We filtered the articles to include only biographies using the `Biography` mark in the Wikipedia metadata, and the parallel ZH-EN articles were further filtered with the `translation` mark. 

- Data Collection and Cleaning: We used in-house scripts to do the above filtering operations and data cleaning.

- Sentence Alignment: For better alignment accuracy, we at first use a in-house pre-trained ZH-EN NMT model to translate ZH sentences back to EN, and then align EN and ZH sentences using the real EN and translated EN sentences from ZH using the [Hunalign](http://mokk.bme.hu/en/resources/hunalign/) toolkit. And note that we don't allow the allignment across the original section boundaries in the articles.

- Quality Control: Part of the automatically aligned sentences is manually corrected by several bilingual volunteer annotators (see 
[Contributors](##Contributors)), while the rest is filtered automatically through the confidence score provided by Hunalign (score higher than 1.0). Although different levels of checking is employed, the aligned sentences still contain some unavoidable noise, such as omissions, additions and paraphrasing. 


## Quick Look
Each line in the file is separated by tab, which consists 9 columns. 
```
2	Marx was ethnically Jewish. His maternal grandfather was a Dutch rabbi, while his paternal line had supplied Trier's rabbis since 1723, a role taken by his grandfather Meier Halevi Marx.	1 ::: 1	Biography ::: Childhood and early education: 1818–1836	1	馬克思的祖先為猶太人，他的外祖父是一名荷蘭拉比；而他的父系祖譜从1723年開始便一直擔任特里爾當地的拉比職務，一直延續到他的祖父梅爾·哈勒維·馬克思。	1 ::: 1	早年 ::: 童年和教育	1
```
Description for each column:

- col 1: article-id (both zh2en and en2zh articles start numbering from 0)
- col 2: EN text
- col 3: EN section-id (the hierarchical numbering is preversed)
- col 4: EN section heading
- col 5: EN sentence-id
- col 6: ZH text
- col 7: ZH section-id
- col 8: ZH section heading
- col 9: ZH sentence-id

### Data Summary
| FileName       | # Sentence  |  Notes    |
| -------------  |:----------:|:-----------:|
| en2zh-auto.txt | 22056      |   automatically filtered, originally written in English and translated into Chinese  |
| en2zh-human.txt| 7616       |   human-checked,  originally written in English and translated into Chinese          |
| zh2en-human.txt| 875        |   human-checked,  originally written in Chinese and translated into English          |



## Contributors

Thanks for the following voulunteer annotators for their contributions in labelling aligned sentences:
- [Mandy Xuqi Li](https://github.com/Mandyli1996) 
- [Yusheng Tian](https://www.linkedin.com/in/yusheng-tian/)
- [Iris Zipei Wang](https://github.com/iriskarling)
- [Chengyu Wu](https://www.linkedin.com/in/城宇-吴-a60963191/)
