# 希尔排序：ShellSort

* 希尔排序\(交换\):
  * 将数组按一定数量分组，从arr.length/2，以此类推每次除2
  * 在同组之间进行插入排序
  * 当分组数量=1时，正好分为一组，算法终止

```java
public class ShellSort {
    public void shellSort(int[] arr){
        //1.校准
        int len = arr.length;
        if(len <= 1){
            return;
        }
        //2.将数组按一定数量分组，每次循环为上次分组的1/2;
        int temp = 0;
        //2.1 分组数量递减，gap为分组数量
        for (int gap = len / 2; gap > 0; gap /= 2) {
            //2.2 i从第gap个数开始，分别与同一组的其他数作比较
            for (int i = gap; i < len; i++) {
                //2.3 当前数：i 与同组的上一个数：j=i-gap比较，如果上一个数比当前数大则交换
                //形成有小到大排序
                for (int j = i - gap; j >= 0; j -= gap) {
                    if (arr[j] > arr[j + gap]) {
                        temp = arr[j];
                        arr[j] = arr[j + gap];
                        arr[j + gap] = temp;
                    }
                }
            }
        }
    }

    @Test
    public void testBubbleSort() {
        int[] array = new int[7];
        array[0] = 5;
        array[1] = 2;
        array[2] = 6;
        array[3] = 9;
        array[4] = 0;
        array[5] = 3;
        array[6] = 4;
        System.out.println(Arrays.toString(array));
        shellSort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

* 希尔排序\(移动\)-更快

```java
public void shellSort2(int[] arr) {
        //1.校准
        int len = arr.length;
        if(len <= 1){
            return;
        }
        for (int gap = len / 2; gap > 0; gap /= 2) {
            //2.从第gap个元素，逐个对坐在组做插入排序
            for (int i = gap; i < len; i++) {
                //2.1 这里current指向当前元素(索引)
                int current = i;
                // temp为当前元素数值
                int temp = arr[current];
                //2.2 如果当前元素比上一个组内元素小再进行下一步(貌似可以省略)
                if (arr[current] < arr[current - gap]) {
                    //2.3 保证索引>=0; 当前值比上一个值小（才移动)
                    while (current - gap >= 0 && temp < arr[current - gap]) {
                        //2.4 想插入排序一样，把大的数依次后移
                        arr[current] = arr[current - gap];
                        current -= gap;
                    }
                    //2.5 将当前数放到应在的位置上
                    arr[current] = temp;
                }
            }
        }
    }
```

