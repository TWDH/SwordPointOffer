# 插入排序：InsertionSort

* **InsertionSort**
  * 从第一个元素开始，该元素可以认为已经被排序；
  * 取出下一个元素，在已经排序的元素序列中从后向前扫描；
  * 如果该元素（已排序）大于新元素，将该元素移到下一位置；
  * 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置；
  * 将新元素插入到该位置后；
  * 重复步骤2~5

```java
public class InsertionSort {
    public void insertionSort(int[] arr){
        //1.校验
        int len = arr.length;
        if(len <= 1){
            return;
        }
        //2.将array中第一个数字设为已排序区间，并从第一个数字向后遍历
        for (int i = 1; i < len; i++) {
            //2.1 将未排序区间的第一个数（i）设置为current
            int current = arr[i];
            //2.2 这里preIndex指向已排序区间的最后一个数
            int preIndex = i - 1;
            //2.3 在已排序区间从后向前扫描，如果已排序区间的数大于当前数，则把这个大的数向后移动一位，
            // 直到已排序区间的数<=当前数
            while (preIndex >= 0 && arr[preIndex] > current) {
                arr[preIndex + 1] = arr[preIndex];
                preIndex--;
            }
            //2.4把当前数放到上面已经腾好的位置中
            arr[preIndex + 1] = current;
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
        insertionSort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

