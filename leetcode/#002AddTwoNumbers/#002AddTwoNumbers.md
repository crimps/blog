##问题描述
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input** : (2 -> 4 -> 3) + (5 -> 6 -> 4)

**Output** : 7 -> 0 -> 8

##问题解析
非负链表，以反向排列来表示数值，（2 -> 4 -> 3）表示342，（5 -> 6 -> 4)表示465，342与465相加的结果为807，所以最终要求的结果就是(7 -> 0 -> 8).
由于链表是反向，因此数值运算从个位开始也就是从链表第一位开始相加，如果大于10则进位，然后进行第二位的相加，以此类推直到最后一位。
要点：
1. 要注意的就是一些特殊情况，比如说两个链表不等长的情况，还有就是最后一位的高位进位要考虑。
2. 对于链表的处理也是个重点，用链表的尾插法来处理是个人认为比较好的方式，但是下面给出的示例代码并没有有尾插法来做，那只是个人的偷懒（PS:好吧说实话，那时写的时候忘了尾插法是怎么实现的了，后面一定找个时间用尾插法重新实现一遍）。

##示例代码
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //进位标识
        boolean carryFlag = false;
        //补高位标识
        boolean highFlag = false;
        List<ListNode> listNodes = new ArrayList<>();
        ListNode p1 = l1;
        ListNode p2 = l2;
        while (null != p1 || null != p2) {
            int value1 = 0;
            int value2 = 0;
            if (null != p1) {
                value1 = p1.val;
            }
            if (null != p2) {
                value2 = p2.val;
            }
            int value = value1 + value2;
            if (carryFlag) {
                value = value + 1;
                //进位标识清空
                carryFlag = false;
            }

            //进位处理
            if (value > 9) {
                value = value % 10;
                carryFlag = true;
                //高位为空时，新增高位处理
                if (((null != p1 && null == p1.next) && (null == p2 || null == p2.next)) || ((null != p2 && null == p2.next) && (null == p1))) {
                    highFlag = true;
                }
            }
            listNodes.add(new ListNode(value));

            //链表后移处理
            if (null != p1 && null != p1.next) {
                p1 = p1.next;
            } else {
                p1 = null;
            }
            if (null != p2 && null != p2.next) {
                p2 = p2.next;
            } else {
                p2 = null;
            }
        }
        //最后新增高位
        if(highFlag) {
            listNodes.add(new ListNode(1));
        }

        for (int i = 0; i < listNodes.size() - 1; i++) {
            listNodes.get(i).next = listNodes.get(i + 1);
        }

        return listNodes.get(0);
    }


