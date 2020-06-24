# 回文经典Manacher
### 解决问题：查找最长回文子串

* 步骤：
1. 处理原始字符串S（abccbba），同步奇偶差异S（#a#b#c#c#b#b#a#）。
2. 两个指针，center为遍历位置中心点，right为遍历过的出现回文最右边界。
3. 一个数组，记录字符串下标对应的回文半径。
4. 遍历开始
```
	radius = array();
	cneter = 0;
	right = 0;
	for(i=0;i<length(S);i++){
		//判断临界,当前中心点在最右边界
		if(i<right){
			radius[i] = min(right-i, radius[2*center-i]) //2*center-i 为i的对称点
		}
		//以中心向两边扩散
		while(S[i+radius[i]+1] == S[i-radius[i]-1]){ //radius[0]从0开始，+1和-1分别
			radius[i]++
		}
		//移动right
		if(i+radius[i]>right){
			center = i
			right = i+radius[i]
		}
	}
	
	//radius中半径最大的，即为结果
```
