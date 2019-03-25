
# Learned Indexes
The code is based from https://github.com/yangjufo/Learned-Indexes

Implementation of BTree part for paper 'The Case for Learned Index Structures'.  

T. Kraska, A. Beutel, E. H. Chi, J. Dean, and N. Polyzotis. The Case for Learned
Index Structures. https://arxiv.org/abs/1712.01208, 2017
>Language: Python  
Support content: Integer values, Random and Exponential distribution

## Files Structures
> data/: test data  
model/: learned NN model  
perfromance/：NN and BTree performance  
Learned_BTree.py: main file  
Trained_NN.py: NN structures

## HOW TO RUN
> First, you need to install python2.7.x and package tensorflow, pandas, numpy, enum.   
Second, use command to run the Learned_BTree.py fule, that is,  
```python Learned_BTree.py -t <Type> -d <Distribution> [-p|-n] [Percent]|[Number] [-c] [New data] [-h]```.  
  
>Parameters:  
'type': 'Type: sample, full',  
'distribution': 'Distribution: random, exponential',  
'percent': 'Percent: 0.1-1.0, default value = 0.5; sample train data size = 300,000',  
'number': 'Number: 10,000-10,000,000, default value = 300,000',  
'new data' 'New Data: INTEGER, 0 for no creating new data file, others for creating'  
  
>Example:  
```python Learned_BTree.py -t full -d random -n 100000 -c 1```  
  

## Other Content
### Sample Training
> Sample training is also included in this project, you can use parameter 'sample' for '-t' to test sample training, while '-p' is used for change the sample training percent.  
  
>Example:  
```python Learned_BTree.py -t sample -d random -p 0.3 -c 0```
### Storage Optimization
>More Information will be added soon.

![Stage Models](https://github.com/yangjufo/Learned-Indexes/blob/master/about/models.PNG)
``` 
 Input: int threshold, int stages[]
 Data: record data[]
 Result: trained index
1 M = stages.size;
2 tmp_records[][];
3 tmp_records[1][1] = all_data;
4 for i ← 1 to M do
5   for j ← 1 to stages[i] do
6     index[i][j] = new NN trained on tmp.records[i][j];
7     if i < M then
8       for r ∈ tmp.records[i][j] do
9         𝑞 = f(r.key) / stages[i + 1];
10        tmp.records[i + 1][ 𝑞].add(r);
11 for j ← 1 to index[M].size do
12   index[M][j].calc_err(tmp.records[M][j]);
13   if index[M][j].max_abs_err > threshold then
14     index[M][j] = new B-Tree trained on tmp_records[M][j];
15 return index;
```
