---
layout: post
title: "Why not use Excel to view Genomic data files"
date: 2020-11-20 00:00:00
description: Excel misreads some gene names as DateTime values. What is the consequence?
img: 
fig-caption: # Add figcaption (optional)
tags: [bioinformatics, genomic, Excel, misread, datetime]
---
I am working on a Bioinformatics paper at UniSA DAG. TO be clear, I am not the first author of the paper but continuing it. My responsibilities are to re-run experiments and to review code implementation. While going through the source code, I accidentally checked a CSV file that contains gene names, and found a really weird name, 6-sept. I was gobsmacked at first glance but swiftly recall an article not too long ago about Biology scientists rename gene names because Microsoft Excel recognizes some of them as DateTime values.

After surfing the internet shortly, here is the [article](https://www.theverge.com/2020/8/6/21355674/human-genes-rename-microsoft-excel-misreading-dates?fbclid=IwAR1iEd6eHMrRgvRSKYvTj8s3YeAvvw2exESlzAP0IQ6F8eCMTNPx9bIUduc) I mentioned. It is clear to say that the predecessors did not revise gene names after saving them to a CSV file by any mean. Unfortunately, the misread gene name lies close to the bottom of the file, so it is hard to spot the strange after a glance. It did not take me long to find the correct name of the misread, and it is SEPT6. Although there is only 1 gene name was misread, the experiment bears the consequences of missing 1 matched gene. The draft of the paper was filled with the result of missing SEPT6, thus must be substituted.

However, let’s create a simple dataframe with 1 row containing SEPT6 as GeneName, for example. Everything seems right unless we open it in Excel. If you open it with Excel, it’ll be fine as long as you don’t save it. However, it can be opened in Excel by someone such as teammates, supervisors, or reviewers. If they unintentionally re-save it, from that point, SEPT6 is misread as 6-Sep. Therefore, my suggestion is to save genomic data as RData if we use R, any type except XLS/XLSX and CSV, or do not use Excel to view.

```
df <- as.data.frame(list('SEPT6', 1.0))
colnames(df) <- c('GeneName', 'SomeData')

write.csv(df, file='~/SomeWhereInYourComputer/gene_data.csv')
```

| ![In R](/assets/img/20201120-donot-use-excel-to-view-genomic-data-files/in_R.png) | 
|:--:| 
| *Figure 1: The dataframe viewed in R* |

| ![In TextEdit](/assets/img/20201120-donot-use-excel-to-view-genomic-data-files/in_textedit.png) | 
|:--:| 
| *Figure 2: The dataframe viewed in TextEdit on Mac* |

| ![In SpreadSheet](/assets/img/20201120-donot-use-excel-to-view-genomic-data-files/in_spreadsheet.png) | 
|:--:| 
| *Figure 3: The dataframe viewed in Spreadsheet on Google Drive* |

| ![In Excel](/assets/img/20201120-donot-use-excel-to-view-genomic-data-files/in_Excel.png) | 
|:--:| 
| *Figure 4: The dataframe viewed in Excel* |


Please let me know if you have a better idea. Cheers!