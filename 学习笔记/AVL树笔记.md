
今天做习题的时候碰到了如下题目：
Click the AVL tree that results when 5, 3, 2, 6, 8, 9, 10, 17, 15, 14, 12 are inserted, in that order, into an initially empty tree.

解题过程如下（字丑，方框表示异常点）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190503163941859.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNzc4MTU3OA==,size_16,color_FFFFFF,t_70)
在完成此题时，由于对AVL树的重平衡不熟悉，还是费了一点时间才把题目做出了，在此过程中参考了网上一些文章，对AVL的旋转有了新的认识和理解，学习及记录如下（以下内容参考自https://www.jianshu.com/p/65c90aa1236d，如有侵权，请联系删除）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190503164224685.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNzc4MTU3OA==,size_16,color_FFFFFF,t_70)
在AVL树的插入中，一般会遇到这四种情况，其实case1和case4可以通过单次旋转实现重平衡，而case2和case3则需要通过两次旋转实现重平衡。（图中的z表示第一个不平衡点，y表示插入元素时访问z之后访问的点，x表示插入元素时访问y之后访问的点。）

**单次旋转(singly rotatioin)**
单次旋转得到重新平衡的子树的示意图如下所示，需要注意的是分清对应的结点。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190503164800287.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNzc4MTU3OA==,size_16,color_FFFFFF,t_70)

**双次旋转(doubly rotatioin)**
case2情况下，需要先对y结点进行一次左旋转，然后再对z结点进行一次右旋转；
case3情况下，需要先对y结点进行一次右旋转，然后再对z结点进行一次左旋转；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190503164859916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNzc4MTU3OA==,size_16,color_FFFFFF,t_70)