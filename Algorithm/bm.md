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
  
  for(int i=0; i<b.length; i++){
    int j=i;
    int k=0;
    while(){
      
    }
  }
}
```





