# 选择排序：SelectionSort

* SelectionSort
  * 把数组第一个数假定为最小值
  * 依次比较此数和后面每一个数的大小，找到最小值，并与第一个数交换。这时，第一个数为最小值
  * 以此类推，直到数组由小到大排列

```java
public class SelectionSort {
    public void selectionSort(int[] arr) {
        //1.校验
        int len = arr.length;
        if(len <= 1){
            return;
        }
        //2.遍历数组，把最小的数依次交换到最前端
        for (int i = 0; i < len - 1; i++) {
            int minIndex = i;
            //2.1 如果碰到比第一个数小的数，则交换
            for (int j = i; j < len; j++) {
                if(arr[j] < arr[minIndex]){
                    minIndex = j;

                }
            }
            //交换实际最小值和已排序空间假定的最小值
            if(minIndex != i){
                //arr[i]:已排序序列的第i个值
                //arr[minIndex]:未排序序列的最小值
                int current = arr[i];
                arr[i] = arr[minIndex];
                arr[minIndex] = current;
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
        selectionSort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

