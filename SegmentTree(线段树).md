# 线段树

---

## 说明：

> 线段树模板

## Java代码模板：

```java

import java.util.Scanner;

/**
 * @description: 线段树
 * 这个模板主要展示了基本的构建，以及一些基本的使用，详细的使用需要通过题目要求动态修改。
 * @author 长白崎
 * @date 2023/5/2 1:54
 * @version 1.0
 */
public class SegmentTree {


    public static void main(String[] args) {

        //测试数据
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int data[] = new int[n+1];
        int tree[] = new int[(n+1)*4];

        for(int i= 1 ; i <=n ; ++i){
            data[i] = sc.nextInt();
        }
        build(tree,data,1,1,n);

        int start =  sc.nextInt();
        int end = sc.nextInt();
        System.out.println(query(tree,start,end,1,1,n));
    }

    /**
     * 获取当前节点编号的左儿子结点编号
     * @param p 代表当前结点的标签序号
     * @return 返回其左子节点的标签号
     */
    public static int ls(int p){
        return p<<1;
    }

    /**
     * 获取当前结点编号的右儿子结点编号
     * @param p 代表当前结点的标签序号
     * @return 代表其右子结点的标签号
     */
    public static int rs(int p){
        return p<<1|1;
    }

    /**
     * 用于计算当前结点所对应的左右子结点的总和
     * @param tree 所构建的线段树
     * @param p 表示我们需要计算的结点的标签
     */
    public static void pushUp(int tree[],int p){
        tree[p] = tree[ls(p)] + tree[rs(p)]; //区间和
    }
    /**
     * 构建线段树
     * @param tree
     * @param left
     * @param right
     */
    public static void build(int tree[],int data[],int p,int left,int right){
        if(left == right){
            tree[p] = data[left];
            return;
        }

        int mid = (left+right) >>1;
        build(tree,data,ls(p),left,mid);
        build(tree,data,rs(p),mid+1,right);
        pushUp(tree,p);
    }

    /**
     * 区间和查询
     * @param tree 构建的线段树
     * @param L 代表我们需要查询的数组对应的区间左标
     * @param R 代表我们需要查询的数组对应的区间右标
     * @param p 代表的是我们当前的所查询基于的父节点的结点标签
     * @param ls 代表当前父结点的范围左标
     * @param rs 代表当前父结点的范围右标
     * @return 返回最终的区间总和值
     */
    public static int query(int tree[],int L,int R,int p ,int ls,int rs){
        //完全覆盖
        if(L <= ls && R >= rs) return tree[p];
        int res =0;
        int mid = (ls+rs) >> 1;
        if(L <= mid) res+= query(tree,L,R,ls(p),ls,mid);
        if(R > mid)  res+= query(tree,L,R,rs(p),mid+1,rs);
        return res;
    }

}

```

