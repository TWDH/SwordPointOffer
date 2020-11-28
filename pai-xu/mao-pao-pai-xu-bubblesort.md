# 冒泡排序：BubbleSort

* **BubbleSort**

  1. 比较两个相邻元素。如果第一个比第二个大，就交换他们两个；
  2. 对每一对相邻元素做相同的工作，从第一队到结尾的最后一对，这样在最后的元素为最大数；
  3. 针对所有元素重复以上步骤，除了最后一个；
  4. 重复以上步骤，直到排序完成

  * 注意：每次排序都只会把一个元素（最大）送到末尾，有n个数需要重复（n-1）次

```java
public class BubbleSort {
    public void bubbleSort(int[] arr){
        int len = arr.length;
        //1.校验
        if(len <= 1){
            return;
        }
        //2.一共进行多少次排序
        for(int i=0; i < len-1; i++){
            //2.1 每次把一个最大数放到最后
            for(int j=0; j < len-i-1; j++){
                if(arr[j] > arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
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
        bubbleSort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

