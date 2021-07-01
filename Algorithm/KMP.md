```java
/**
* @param a 主串
* @param b 模式串
*/
public static int kmp(char[] a, char[] b){
  int[] next = getNexts(b);
  int j=0; // j 模式串下标
  for(int i=0 ; i<a.length; i++){ // i 主串下标
    // i,j 此时表示需要匹配的下标
    while(j>0 && a[i]!=b[j]){ // 一直找到a[i] == b[j] || j<=0
      j = next[j-1]+i; // j 回退到前缀匹配next[j-1],然后查看next[j-1]+1是否与a[i]相同
    }
    if(a[i] == b[i]){// 寻找 a[i] == b[0] || a[i] == b[j]
      j++;
    }
    if(j == b.length){// b下标j已经匹配完成，超过b.length-1
      return i-b.length+1;// i-(b.length-1)
    }
  }// i 遍历a完成，对于a的每一位，未找到j满足j == b.length
    return -1;
}
```

### 失效函数的计算

next数组是对于模式串而言的。P 的 next 数组定义为：next[i] 表示 P[0] ~ P[i] 这一个子串，使得 **前k个字符**恰等于**后k个字符** 的最大的k，前K个字符下标

```java
private static int[] getNexts(char[] b){
  int[] next = new int[b.length];
  next[0] = -1;
  int k= -1;
  for(int i=1; i<b.length; i++){
    // k 前缀下标，i为模式串下标+1
    while(k != -1 && b[k+1]!=b[i]){ // 寻找b[k+1] == b[i] 
      k = next[k]; // k 回退
    }
    if(b[k+1] == b[i]){// 寻找 b[0]== b[i] || b[k+1] == b[i]
      ++k;
    }
    next[i]=k;
  }
}
```



```java
private int[] getNext(char[] b){
  int[] next = new int[b.length];
  next[0] = -1;
  int k = -1;
  
  for(int i=1; i<b.length; i++){
    while(k!=-1 && b[k+1]!=b[i]){
      k = next[k];
    }
    if(b[k+1] == b[i]){
      k++;
    }
    next[i] = k;
  }
}

public int kmp(char[] a, char[] b){
  int[] next = getNext(b);
  int j=0;
  for(int i=0; i<a.length; i++){
    while(j>0 && b[j]!=a[i]){
      j = next[j-1]+1;
    }
    if(b[j] == b[i]){
      j++;
    }
    if(j == b.length){
      return i-b.length+1;
    }
  }
}
```



```java
private int[] getNext(char[] b){
  int[] next = new int[b.length];
  next[0] = -1;
  int k = -1;
  for(int i=1; i<b.length; i++){
    // k 前缀下标，i为模式串下标+1
    while(k!=-1 && b[k+1]!=b[i]){ // 寻找b[k+1] == b[i] 
      k = next[k]; // k回退，ensure b[0,k] match b[~,i-1]
    }
    if(b[k+1] == b[i]){ // 寻找 b[0]== b[i] || b[k+1] == b[i]
      k++;
    }
    next[i] = k;
  }
}

public int kmp(char[] a, char[] b){
  	int[] next = getNext(b);
  	int j=0; // b index
  	for(int i=0; i<a.length; i++){// a index
      while(j>0 && b[j] !=a[i]){
        j = next[j-1]+1;// ensure b[0,j-1] match a[~,i-1]
      }
      if(b[j] == a[i]){ // ensure b[0,j] match a[~,i]
        j++;
      }
      if(j == b.length){
        return i-b.lenth+1;
      }
    }
  return -1;
}
```



```java
// kmp 
/**
* next[i]=k b[0,i]的后缀子串中，匹配的最长前缀结束下标为k，则k+1位的后缀b[i-k,i] 与b[0,k]相同
*/
public int[] getNext(char[] b){
  int[] next = new int[b.length];
  int k = -1;
  for(int i=1; i<b.length; i++){
    while(k!=-1 && b[k+1]!=b[i]){
      k = next[k];
    }
    if(b[k+1] == b[i]){
      k++;
    }
    next[i] = k;
  }
}
```



```java
public int[] getNext(char[] b){
  int[] next = new int[b.length];
  int k=-1;
  for(int i=0; i<b.length; i++){
    while(k!=-1 && b[k+1]!=b[i]){
      k = next[k];
    }
    if(b[k+1] == b[i]){
			k++;
    }
    next[i] =k;
  }
  return next;
}
```



```java
/**
* @return next[i]=k 最大前缀下标k
*/
public int[] getNext(char[] b){
  int[] next = new int[b.length];
  next[0] = -1;
 	int k =-1;
  for(int i=1; i<b.length; i++){
    while(k!=-1 && b[k+1] == b[i]){
      k = next[k];
    }
    if(b[k+1] == b[i]){
      k++;
    }
    next[i]=k;
  }
  return next;
}

public int kmp(char[] a, char[] b){
  int[] next = getNext(b);
  int j=0;
  for(int i=0;i<a.length; i++){
    while(j>0 && b[j]!=a[i]){
      j = next[j-1]+1;
    }
    if(b[j] == a[i]){
      j++;
    }
    if(j == a.length){
      return i-b.length+1;
    }
  }
  return -1;
}

```

