# 面试题39： 数组中出现次数超过一半的数字

## 方法一：HashMap

1. 创建`HashMap<Integer, Integer>`（数字，次数）
2. 遍历数组
   1. 如果`num[i]`在map中，则将其对应的值**+1**
   2. 如果`num[i]`不在map中，则将其值设为**1**
3. 遍历map，找出次数大于数组一般的并返回。

```java
public int majorityElement(int[] nums) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for(int i=0; i<nums.length; i++){
        if(map.containsKey(nums[i])){
            //map中存过此数
            int temp = map.get(nums[i]);
            map.put(nums[i], temp + 1);
        }
        else{
            //没有存过此数
            map.put(nums[i], 1);
        }
    }

    //遍历map
    for(Integer i: map.keySet()){
        if(map.get(i) * 2 > nums.length){
            return i;
        }
    }
    return 0;
}
```

## 方法二：**摩尔投票法**

* 票数和：永远&gt;=0，因为众数出现次数超过数组的一半
  * **众票**：+1
  * **非众票**：-1
* 票数正负抵消：
  * 如果vote=0，设当前元素n1为众数，下一个数如果与n1不相等则抵消vote-1，否则vote+1。
  * 每次vote=0时，才更改众数
  * `num == x` ---&gt; `vote+1`
  * `num != x` ---&gt; `vote-1`

![](../.gitbook/assets/image%20%2818%29.png)

```java
public int majorityElement(int[] nums) {
    int vote = 0;
    int x = 0;
    for(int num : nums){
        if(vote == 0){
            x = num;
        }
        if(num == x){
            vote += 1;
        }
        else{
            vote -= 1;
        }
    }
    return x;
}
```

