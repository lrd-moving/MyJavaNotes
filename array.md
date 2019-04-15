package com.Lrd;


import com.sun.javafx.binding.StringFormatter;

import java.io.OutputStream;
import java.sql.SQLOutput;
import java.util.*;

public class ArrayTest {
    public static void main(String[] args) {
        //1. 两种声明方式
        int[] test1 = new int[5];
        int[] test2 = {2, 1, 3, 4, 5};
        String[] teststr = {"1", "2", "3"};

        //2. 查看数组长度
        System.out.println("Array length = " + test1.length);

        //3. 遍历数组
        for (int i : test2) {
            System.out.println("Array element = " + i);
        }

        //4. int数组转成String数组
        String[] test3 = new String[test2.length];
        int i;
        for (i = 0; i < test2.length; i++) {
            test3[i] = Integer.toString(test2[i]);
        }
        System.out.println("int to String = " + test3.toString());

        //5.  从array中创建arraylist(String)
        ArrayList<String> list = new ArrayList<String>();
        Collections.addAll(list, teststr);
        System.out.println("array to list = " + list.toString());


        //6. 从array中穿件ArrayList(int)
        //java集合框架数据结构中元素不能为基础类型（int,char）需要转一下。
        //使用common-lang3可以快速转化， 详见 https://blog.csdn.net/makanglei1994/article/details/82881679
        ArrayList list2 = new ArrayList();
        Integer[] IntArray = new Integer[test1.length];
        for (i = 0; i < test1.length; i++) {
            IntArray[i] = test1[i];
        }
        System.out.println("array to list = " + Arrays.toString(IntArray));

        //6. 测试数组溢出
        /*
        System.out.println("test1's length = " + test1.length);
        try {
            System.out.println("try to access test[" + test1.length + "]...");
            System.out.println(test1[test1.length]);
        } catch (Exception e) {
            System.out.println(e.toString());
            e.printStackTrace();
        }
        */

        //7.1  数组中是否包含某个值,使用sort+binarySearch
        Arrays.sort(test2);
        System.out.println("test2 after sort" + Arrays.toString(test2));
        int pos = Arrays.binarySearch(test2, 2);
        if (-1 == pos) {
            System.out.println("Not find");
        } else {
            System.out.println("Find, pos:" + pos);
        }

        //7.2 数组中是否包含某个值,借助于list结构
        System.out.println("array to list = " + array2List(test2).toString());
        System.out.println("Find status = " + array2List(test2).contains(2));

        //8. 数组转化为set集合
        HashSet set = new HashSet(array2List(test2));
        System.out.println("Hashset = " + set.toString());


        //9. Array的填充
        Arrays.fill(test2, 1);
        System.out.println("Array fill 1" + Arrays.toString(test2));

        //10. 数组的排序
        for (int j = 0; j < test2.length; j++) {
            test2[j] = 10 - j;
        }
        System.out.println("Sort test2 before = " + Arrays.toString(test2));
        Arrays.sort(test2);
        System.out.println("Sort test2 after = " + Arrays.toString(test2));

        //11.复制数组
        int[] test22 = Arrays.copyOf(test2, test2.length);
        System.out.println("Copy test22 = " + Arrays.toString(test2));

        //12. 比较两个数组
        System.out.println("Compare test2 and test22 = " + Arrays.equals(test2, test22));
        test22[1] = 100;
        System.out.println("Compare test2 and test22 = " + Arrays.equals(test2, test22));

        //13. 去重复
        test22[2] = 100;
        set.clear();
        System.out.println("Remove same before = " + set.toString());
        for (int element : test22){
            set.add(element);
        }
        System.out.println("Remove same after = " + set.toString());

        //14.查询数组中最大值和最小值
        int max = test22[0];
        for (int element : test22){
            max = Integer.max(element, max);
        }
        System.out.println("max = " + max);
    }
    private static List array2List(int[] array){

        Integer[] IntArray = new Integer[array.length];

        for (int i = 0; i < array.length; i++) {
            IntArray[i] = array[i];
        }

        return Arrays.asList(IntArray);
    }

}
