# 大名鼎鼎KMP
### 解决问题：查找一个字符串S中是否存在另一个字符串P
* 例如：
```
 S = 'abcacabcabde'
 P = 'abcabd'
 查找P存在于S中的位置
```
* **步骤**
1. 通过匹配串P，获取其对应的next数组。
2. 遍历目标S串，在匹配的过程中引入next数组，以便减少查询。

* **开门见山**
```
  next获取（当前字符之前的字符串M，查找M前和后存在长度最长的相同的子字符串长度）：
  
  P = 'abcabd' //长度为6
  
  Array next = [0,0,0,0,0,0];
  
  next[0] => '' //'a'之前为空字符'',故 next[0] = 0
  
  next[1] => 'a' //位置1之前的字符串为'a','a'是一个单字符，故next[1] = 0
  
  //next前两个元素是固定的值，都为0
  
  next[2] => 'ab' //位置2之前的字符串为'ab', 'a' != 'b',故 next[2] = 0
  
  next[3] => 'abc' //位置3之前的字符串为'abc', 'a' != 'c' && 'ab' != 'bc' ,故 next[3] = 0
  
  next[4] => 'abca' //位置4之前的字符串为'abca',此时首尾都为'a',但是'ab' != 'ca'、'abc' != 'bca' ,故 next[4] = 1 ('a'的长度)
  
  next[5] => 'abcab' //位置5之前的字符串为'abcab',此时首尾都为'ab',但是'abc' != 'cab'、'abca' != 'bcab' ,故 next[5] = 2（'ab'的长度）
  
```
* **代码实现-next**
```
  next = make(0,length(P)) //生成长度为P长度的数组
  //遍历
  j = 0;
  //i从2开始
  for(i=2;i<length(P);i++){
    //j不等于0，意味着j之前的存在next值大于0的元素
    //P[j]!=P[i-1],如abcabd中 c!=d
    if (j!=0 && P[j] != P[i-1])
        j = next[i-1]
    //P[j]==P[i-1]，例如abab,匹配完a=a后，接着判断b=b,那么j就加1
    if  P[j] == P[i-1]
        j++
    //给next赋值
    next[i] = j
  }
```
* **拨云见雾**
* 已经获取到了next后，开始处理目标字符串S
1. 遍历字符串S，如果S串和P串匹配第一位，P串指针后移一位
2. 后移过程中，如果失配了，将j的位置移动到next对应的value处（next数组的用处，如果没有next数组，每次失配需要将j移动到第一位重新开始）
3. 如果j==length(P) ，匹配成功

* **匹配代码**
```
  j = 0
  for(i=0;i<length(S);i++){
    //失配处理
    while(j>0 && S[i] != P[j])
      j = next[j]
    //匹配上
    if (S[i] == P[j]) 
      j++
    //成功
    if (j == length(P))
      return i-length(P)+1
  }
```
