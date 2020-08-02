## 第一周学习笔记

**刻意练习**

拆分知识点、重复练习、反馈



**【拆分知识点】**





**【如何重复练习】**

**五毒神掌（五步刷题法）**

**刷题第一遍：**

- 5分钟读题+思考
- 直接看解法，注意多解法，比较解法优劣
- 背诵、默写好的解法
- 不要纠结、不要抢救

**刷题第二遍：**

- 马上自己写，在leecode上提交
- 多种解法比较体会优化

**刷题第三遍：**

- 过一天后，再重复做题
- 不同解法的熟练程度，专项练习

**刷题第四遍：**

- 过一周，再回来练习相同的题目

**刷题第五遍：**

- 面试前一周恢复性训练



**【如何获取反馈】**

- 即时反馈
- 主动找反馈（高手代码 github、leetcode,第一视角直播）
- 被动型反馈（code review）


> 盛最多水的容器

题目很好理解，最多水 = Min(an,am)*(m-n)  其中m>n

主要需要理解的是



```java
   public int maxArea(int[] height) {

        int max = 0;
        int i = 0, j = height.length - 1;

        while (i < j) {
            int minHeight = height[i] < height[j] ? height[i++] : height[j--];
            int area = minHeight * (j - i + 1);
            max = Math.max(max, area);

        }

      return   max;

    }
```





> 两两交换链表中的节点

注意理解递归，下一次递归的起点是第二个节点的next

```java
  public ListNode swapPairs(ListNode head) {

        //TODO 递归中止条件
        if (head == null || head.next == null) {
            return head;
        }

        ListNode firstNode = head;
        ListNode secondNode = head.next;

        //TODO 下一次递归的起点是第二个节点的next
        firstNode.next = swapPairs(secondNode.next);
        secondNode.next = firstNode;


        return secondNode;
    }
```



> 三数之和

实现思路参考：<https://leetcode-cn.com/problems/3sum/solution/san-shu-zhi-he-cshi-xian-shuang-zhi-zhen-fa-tu-shi/>

讲解的很清楚，看完视频，独立写出来了，不过中间也出几个低级错误，要获取低位指针和高位指针指向的值的地方，传成了指针本身。

**主要理解几个重要的点**：

1. 排序的作用:【1】去重，【2】有利于判断高低指针该如何移动
2. 理解以nums[i]为固定值去寻找其他两个值的一趟循环，命中之后的去重

```java
    public static List<List<Integer>> threeSum(int[] nums) {

        //TODO 二维数组来保存结果
        List<List<Integer>> result = new ArrayList<>();

        //TODO  排序
        Arrays.sort(nums);

        //TODO  遍历寻找
        int possibleSize = nums.length - 2;

        for (int i = 0; i < possibleSize; i++) {

            int nowValue = nums[i];
            int lowPoint = i + 1;
            int hiPoint = nums.length - 1;

            //TODO 以nums[i]为固定值去寻找其他两个值的一趟循环
            while(lowPoint<hiPoint){
                //TODO   这两个值的赋值应该放在while里面，因为每一趟都不一样
                int lowValue = nums[lowPoint];
                int hiValue = nums[hiPoint];

                if (lowValue + hiValue + nowValue == 0) {
                    List<Integer> list = new ArrayList<>();
                    list.add(nowValue);
                    list.add(lowValue);
                    list.add(hiValue);
                    result.add(list);
                    //TODO 继续在【lowpoint,hiPoint】集合中寻找满足的条件 但是要注意去重复项
                    while (lowPoint<hiPoint&&nums[lowPoint]==lowValue) lowPoint++;

                    while (lowPoint<hiPoint&&nums[hiPoint]==hiValue) hiPoint--;

                } else if (hiValue + lowValue + nowValue > 0) {

                    hiPoint--;

                } else {
                    lowPoint++;
                }

            }

            //TODO 去重复，避免先一趟以nums[i+1]为固定值  和 nums[i]  一样
            while(i+1 < possibleSize&&nums[i+1]==nums[i]){
                i++;
            }
        }

        return result;

    }
```



------

**刷题狂魔组练习题目**

> 合并两条有序链表

```java
 public ListNode mergeTwoLists(ListNode l1, ListNode l2) {

        //TODO  辅助节点
        ListNode preHead = new ListNode(-1);
        ListNode pre = preHead;
        //TODO 两个链表都没有遍历到最后一个节点
     //TODO 这里是l1,l2,不是l1.next  l2.next
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                pre.next = l1;
                l1 = l1.next;
            } else {
                pre.next = l2;
                l2 = l2.next;
            }
            pre = pre.next;
        }

        //TODO 两个链表长度不一可能存在一条没合并完的
        pre.next = l1 == null ? l2 : l1;

        return preHead.next;

    }
```

> 猜数字游戏

```java
    public String getHint(String secret, String guess) {

        int bulls = 0;
        int cows = 0;
        //TODO 这个表示secret字符串中0-9的个数，值为负数时表示目前为止guess猜的个数
        int[] nums = new int[10];
        
        for (int i = 0; i < secret.length(); i++) {
            //TODO 字符+索引地址都相等
            char s = secret.charAt(i);
            char g = guess.charAt(i);
            if(s==g){
                bulls++;
            }else{
            //TODO 注意这是后置加
            if(nums[s-'0']++<0) cows++;//++是一定要的操作  <0 表示之前有guess了这个数字
            if(nums[g-'0']-->0) cows++;// >0 表示secret有这个数字，现在guess了这个数字
            }
        }
        
        return bulls+"A"+cows+"B";

    }
```

