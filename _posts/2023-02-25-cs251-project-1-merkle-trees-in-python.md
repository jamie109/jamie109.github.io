---
layout: post
title: "[CS251]project_1: Merkle trees in Python"
date: 2023-02-25 16:16 +0800
author: jamie109
categories: [CS_course, CS251:Cryptocurrencies and Blockchain Technologies]
tags: [Blockchain, projects]
mermaid: true
math: true
---
 
[lab instructions](https://cs251.stanford.edu/hw/proj1.pdf)     

>Your job is to implement the function gen_merkle_proof().    
>The missing code in that function can be implemented in less than ten lines of Python.   

 **Merkle Proof 是 Merkle 树内的一条路径，包含一些节点**：从当前节点（初始为叶子节点，即需要证明的交易）出发，把它的邻居节点加入 Merkle Proof，然后当前节点的哈希与邻居节点的哈希组合，组合后的哈希作为当前节点，此时进入上一层，继续把当前节点的邻居加入路径，并与邻居节点的哈希值组合，更新当前节点，循环，直到到达 root 节点。

简单来说，就是不断把邻居加入 Merkle Proof 的过程，注意叶子节点和 root 节点都不需要加进去。  

* 邻居节点    
  本实验采用二叉 Merkle 树，需要确定当前节点的邻居（跟它同一parent的节点）是在它的左边还是右边。     
  由于每层的节点采用list存储，索引从0开始，另外实验框架中将第一层叶子节点补成了 $2^{height}$ 个，保证之后每层的节点个数都是 $2^{m}$ ，不需要考虑某一层节点个数不够的情况。    
  **如果是当前节点的 index 是奇数，它的邻居索引就是 index-1 ，否则  index+1。**    
  **当前节点的上一层对应的节点索引是 index//2。** 

```python
def gen_merkle_proof(leaves, pos):
    """Takes as input a list of leaves and a leaf position (pos).
       Returns the Merkle proof for the leaf at pos."""
    # 计算 Merkle Tree 的高度
    height = math.ceil(math.log(len(leaves),2))
    assert height < MAXHEIGHT, "Too many leaves."

    # hash all the leaves
    state = list(map(hash_leaf, leaves))  

    # Pad the list of hashed leaves to a power of two
    # state列表末尾添加 padlen个字节的 \x00（空字节），以确保 state 列表的长度是 2^height 的形式
    padlen = (2**height)-len(leaves)
    state += [b"\x00"] * padlen

    # initialize a list that will contain the hashes in the proof
    path = []
    level_pos = pos    # local copy of pos
    # 当前叶子节点的邻居加进去
    # path.append(state[pos])
    if pos % 2 == 0:
        path.append(state[pos + 1])
    else:
        path.append(state[pos - 1])
    # 记录当前层哈希的个数
    this_level_len = len(state)
    for level in range(height-1):
        tmp_state = []
        # 对当前层 state 计算哈希
        for i in range(0, this_level_len - 1, 2):
            tmp_state.append(hash_internal_node(state[i], state[i + 1]))
        # 每向上一层，pos 减半
        level_pos = level_pos // 2
        # 根据 pos 选择要加进来的邻居节点
        if level_pos % 2 == 0:
            path.append(tmp_state[level_pos + 1])
        else:
            path.append(tmp_state[level_pos - 1])
        # 更新 state 和它的长度
        state = tmp_state
        this_level_len = len(state)
    # return a list of hashes that makes up the Merkle proof
    return path
```


