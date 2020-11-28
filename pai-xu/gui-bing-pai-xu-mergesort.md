# 归并排序：MergeSort

* MergeSort
  * 把数组分成左右两边，将两边分别排序
  * 排序后再放到一起（那边小那边放入新数组，如果一边数组为空则直接拷贝另一个数组）

```java
public class MergeSort {
    public int[] mergeSort(int[] arr) {
        //递归跳出条件：分治数组为1时则直接返回
        if (arr.length <= 1) {
            return arr;
        }
        int mid = arr.length / 2;
        int[] left = Arrays.copyOfRange(arr, 0, mid);
        int[] right = Arrays.copyOfRange(arr, mid, arr.length);
        return merge(mergeSort(left), mergeSort(right));
    }

    public int[] merge(int[] left, int[] right) {
        int[] newArray = new int[left.length + right.length];
        //定义指针，代表两个数组下标
        int leftIndex = 0;
        int rightIndex = 0;
        for (int i = 0; i < newArray.length; i++) {
            //左边的数组为空
            if (leftIndex >= left.length) {
                newArray[i] = right[rightIndex++];
            }
            //右面的数组为空
            else if (rightIndex >= right.length) {
                newArray[i] = left[leftIndex++];
            }
            //两面数组都有数
            else if (left[leftIndex] < right[rightIndex]) {
                newArray[i] = left[leftIndex++];
            }
            else {
                newArray[i] = right[rightIndex++];
            }
        }
        return newArray;
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
        array= mergeSort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

* 尚硅谷方法-麻烦

```java
public class MergeSort2 {
    public static void main(String[] args) {
        int arr[] = {8, 5, 3, 7, 1, 3, 6, 2};
        int temp[] = new int[arr.length];
        mergeSort(arr, 0, arr.length-1, temp);
        System.out.println(Arrays.toString(arr));
    }
    public static void mergeSort(int[] arr, int left, int right, int[] temp) {
        //分+合
        if (left < right) {
            int mid = (left + right)/2;
            //递归
            //向左递归分解
            mergeSort(arr, left, mid, temp);
            //向右递归分解
            mergeSort(arr,mid+1, right, temp);
            //合并
            merge(arr, left, mid ,right, temp);
        }
    }

    //合并
    public static void merge(int[] arr, int left, int mid, int right, int[] temp) {
        int i = left; //左边有序序列的初始索引
        int j = mid + 1; // 初始化j，右边有序序列的初始索引
        int t = 0; // 指向temp数组当前索引

        //1.把左右数组填充到temp，知道两边有序序列有一边处理完为止
        while (i <= mid && j <= right) {
            //1.1当左边小时，填入temp
            if (arr[i] < arr[j]) {
                temp[t] = arr[i];
                t++;
                i++;
            }
            else {
                temp[t] = arr[j];
                t++;
                j++;
            }
        }
        //2.把剩余的数据填充到temp
        while (i <= mid) {
            temp[t] = arr[i];
            t++;
            i++;
        }
        while (j <= right) {
            temp[t] = arr[j];
            t++;
            j++;
        }
        //3.将temp拷贝回数组arr
        t = 0;
        int tempLeft = left;
        while (tempLeft <= right) {
            arr[tempLeft] = temp[t];
            t++;
            tempLeft++;
        }
    }
}
```

