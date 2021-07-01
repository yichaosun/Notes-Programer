```java
private static int SIZE = 256;

/**
* char[] b 模式串
* @return 模式串中字符到下标索引
*/
private int[] generateBadCharIndex(char[] b){
		int[] badCharIndex = new int [SIZE];
  	Arrays.fill(badCharIndex,-1);
  	for(int i=0 ; i< b.length ; i++){
      	badCharIndex[(int)b[i]] = i;
    }
  return badCharIndex;
}
```



```java
private static int SIZE = 256;
private int[] generateBC(char[] b){
  int[] bcIndex = new int[SIZE];
  Arrays.fill(bcIndex,-1);
  for(int i=0; i<b.length; i++){
    bcIndex[(int)b[i]] = b[i];
  }
}
```



```java
protected void generateGS(char[] b, int[] suffix, boolean[] prefix){
  Arrays.fill(suffix,-1);
  Arrays.fill(prefix,false);
  
  for(int i=0; i<b.length; i++){ // 好后缀
    int j=i;
    int k=0;
    while( j>= 0 && b[j] == b[b.length-1-k]){
      k++;
      suffix[k] = j;
      j--;
    }
    if(j<0){
      prefix[k]=true; 
    }
  }
}
```



```java
protected void generateGS(char[] b,int[] suffix,boolean[] prefix){
  Arrays.fill(suffix,-1);
  Arrays.fill(prefix,false);
  for(int i=0; i<b.length; i++){
    int j=i;
    int k=0;
    while(j>=0 && b[j] == b[b.length-1-k]){
      k++;
      suffix[k] = j;// 随着遍历，相同的K，会被最右的j覆盖
      j--;
    }
    if(j<0){
      prefix[k] = true;
    }
  }
}
```



```java
private static final int SIZE = 256;
private int[] generateBC(char[] b){
  int[] bcIndex = new int[SIZE];
  Arrays.fill(bcIndex,-1);
  for(int i=0; i<b.length; i++){
    bcIndex[(int)b[i]] = i;
  }
  return bcIndex;
}

private void generateGS(char[] b, int[] suffix, boolean[] prefix){
  Arrays.fill(suffix,-1);
  Arrays.fill(prefix,false);
  
  for(int i=0; i<b.length; i++){
    int j=i;
    int k=0;
    while(j>=0 && b[j] == b[b.length-1-k]){
      k++;
      suffix[k] = j;
      j--;
    }
    if(j<0){
      prefix[k] = true;
    }
  }
}

public int bm(char[] a, char[] b){
  int[] bcIndex = generateBC(b);
  int[] suffix = new int[b.length];
  boolean[] prefix = new boolean[b.length];
  int i=0;
  while(i<= a.length - b.length){
    int j = b.length-1;
   	while(j>=0 && b[j] == a[i+j]){
      j--;
    }
    if(j<0){
      return i;
    }
    int x = j-bcIndex[(int)b[j]];
    int y = 0;
    if(j<b.length-1){
      y = moveByGS(j,b.length,suffix,prefix);
    }
    i = i + math.Max(x,y);
  }
  return -1;
}

protected int moveByGS(int j,int m,int[] suffix,boolean[] prefix){
  int k = m-1-j;
  if(suffix[k] != -1){
    return j-suffix[k]+1; // j - (suffix[k] -1) suffix[k] 好后缀开始，-1即为与坏字符匹配的位置
  }
 	for(int r = j+2; r<=m-1;r++){ // j+1 是好字符下标，
    if(prefix[m-r]){   //  m-1 -(j+1) = m-j-2 = m-(j+2)
      return r; 
    }
  }
  
}
```



```java
protected int moveByGS(int j, int m, int[] suffix, boolean[] prefix){
  int k = m-1-j; // 好后缀长度
  if(suffix[k]!=-1){
    return j-(suffix[k]-1);
  }
  for(int r=j+2; r< m.length; r++){
    if(prefix[m-r]){ // m-1 -r +1
      return r;
    }
  }
  return m;
  
}
```



```java
public int bm(char[] a, char[] b){
  
}

private static final int SIZE = 256;
protected int[] generateBC(char[] b){
  int[] bcIndex = new int();
  Arrays.fill(bcIndex,-1);
  for(int i = 0; i<b.length; i++){
    bcIndex[(int)b[i]] = i;
  }
  return bcIndex;
}

private void generateGS(char[] b, int[] suffix, boolean[] prefix){
  Arrays.fill(suffix,-1);
  Arrays.fill(prefix,false);
  for(int i=0; i<b.length; i++){
    int j=i;
    int k=0;
   	while(j>=0 && b[j] == b[b.length-1-k]){
      k++;
      suffix[k] = j; // 相同k，随着j遍历，将被最右的j覆盖
      j--
    }
    if(j<0){
      prefix[k] = true;
    }
  }
}

private int moveByGS(int j,int m,int[] suffix,boolean[] prefix){
  int k = m-1-j;
  if(suffix[k]!= -1){
    return j+1-suffix[k]; // 好字符串下标差距
  }
  for(int r = j+2; r<m ; r++){
    if(prefix[m-r]){ // m-1-r +1
      return r;
    }
  }
  return m;
}

public int bm(char[] a, char[] b){
  int[] bcIndex = generateBC(b);
  int[] suffix = new int[b.length];
  boolean[] prefix = new boolean[b.length];
  generateGS(b,suffix,prefix);
  int i=0;
  while(i<=a.length - b.length){
    int j=b.length-1;
    while(j>=0 && b[j] == a[i+j]){
      j--;
    }
    if(j<0){
      return i;
    }
    int x = j-bcIndex[(int)b[j]];
    int y = 0;
    if(j<b.length -1){
      y = moveByGS(j,b.length,suffix,prefix);
    }
    i = i+ math.Max(x,y);
  }
  return -1;
}
```



```java
public int bm(char[] a, char[] b){
	int[] bcIndex = generateBC(b);  
  int[] suffix = new int[b.length];
  boolean[] prefix = new boolean[b.length];
  generateGS(b,suffix,prefix);
  int i=0;
  while(i<= a.length - b.length){
    int j=i;
    while(j>=0 && b[j] == a[i+j]){
      j--;
    }
    if(j<0){
      return i;
    }
    int x = j - bcIndex[(int)b[i]];
    int y = 0;
    if(j<b.length-1){// 存在好后缀
      y = moveByGS(j,b.length,suffix,prefix);
    }
    i = i + math.Max(x,j);
  }
  return -1;
}

private static final int SIZE = 256;
private int[] generateBC(char[] b){
  int[] bcIndex = new int[SIZE];
  Arrays.fill(b,-1);
  for(int i=0; i<b.length; i++){
    bcIndex[(int)b[i]]=i;
  }
  return bcIndex;
}

private void generateGS(char[] b, int[] suffix, boolean[] prefix){
  Arrays.fill(suffix,-1);
  Arrays.fill(prefix,false);
  
  for(int i=0; i<b.length; i++){
    int j = i;
    int k = 0;
    while(j>=0 && b[j] == b[b.length-1-k]){
      k++;
      suffix[k] = j;
      j--;
    }
    if(j<0){
      prefix[k] = true;
    }
  }
}

private int moveByGS(int j, int m,int[] suffix, boolean[] prefix){
  int k = m-1-j;
  if(suffix[k]!=-1){
    return j+1-suffix[k];
  }
  for(r=j+2; r<m; r++){
    if(prefix[m-r]){
      return r;
    }
  }
  return m;
}





```





