# 快速排序：QuickSort

* **QuickSort（nlogn ~ n^2）**
  1. 校验：设置递归终止条件
  2. 进行分区（patition）：得到pivot点的index，其左边比他小，右边比他大。
     * 将pivot的值设置为数组最后一个数
     * 将指针设置为第一个位置\(begin\)，该指针用于指向左边小于pivot的数\(随着数的增加向后移动\)
     * 遍历数组，所有小于pivot的数且这些数的index大于pivotIndex的，将当前数和pivotIndex指向的数交换。（注意此时左边无序）
     * 遍历后，所有小于pivot的数都在左边，此时将最后一个pivot与当前pivotIndex所指向的数交换，即可形成       "左 &lt; pivot &lt; 右" 的结构

```java
public class QuickSort {
    //1.从数据序列中找到一个分区点：pivot
    //2.重新排序数列，所有元素和基准点元素比较：比pivot小-左边， 比pivot大-右边
    //3.递归左边和右边
    //注意：pivotIndex左边比起小，右边比其大

    public void quickSort(int[] arr, int begin, int end){
        //1.校验:递归终止条件
        if(arr.length <= 1 || begin >= end){
            return;
        }
        //2.进行分区得到分区下标
        int pivotIndex = partition(arr, begin, end);
        //3.递归：左侧快排
        quickSort(arr, begin, pivotIndex-1);
        //4.递归：右侧快排
        quickSort(arr, pivotIndex+1, end);

    }
    private int partition(int[] arr, int begin, int end){
        int pivot = arr[end];
        int pivotIndex = begin; //pivotIndex指向所有小于pivot的元素
        for (int i = begin; i < end; i++) { //数组全部都遍历-1
            //1.判断如果该区间内有元素小于pivot，则将该元素从区间头开始向后填充
            if (arr[i] < pivot) { //寻找比pivot小的数
                //2.并且当前指针在pivotIndex之后
                if (i > pivotIndex) { //在pivotIndex左边已排序（小），只有右边才需要考虑
                    swap(arr, i, pivotIndex);
                }
                pivotIndex++;
            }
        }
        
        swap(arr, pivotIndex, end); //pivotIndex和pivot交换
        
        return pivotIndex;
    }
    private void swap(int[] arr, int i, int j){
        int temp = arr[j];
        arr[j] = arr[i];
        arr[i] = temp;
    }

    @Test
    public void testQuickSort() {
        int[] array = new int[7];
        array[0] = 5;
        array[1] = 2;
        array[2] = 6;
        array[3] = 9;
        array[4] = 0;
        array[5] = 3;
        array[6] = 4;
        System.out.println(Arrays.toString(array));
        quickSort(array, 0, array.length-1);
        System.out.println(Arrays.toString(array));
    }
}
```

