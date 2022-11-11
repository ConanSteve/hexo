---
title: 维特比算法
date: 2022-02-01 10:00:00
author: 陌上人如玉
mathjax: true
tags: MachineLearning
categories: 
    机器学习笔记
---

Viterbi:DP搜索最优状态序列
定义：Viterbi变量$δ_t(i)$是在时间t时，模型沿着某一条路径到达$S_i$,输出观察序列$Ο=O_1O_2···O_t$的最大概率为：
$$
δ_t(i)=\max_{q_1q_2···q_{t-1}} P(q_1q_2···q_t=S_i, O_1O_2···O_t|i)
$$

[维特比算法实现](https://blog.csdn.net/StarLib/article/details/106904606)

[如何通俗地讲解 viterbi 算法？](https://www.zhihu.com/question/20136144)

```python
from typing import List
import torch


def argmax(vec):
    # return the argmax as a python int
    _, idx = torch.max(vec, 0)
    return idx.item()


def log_sum_exp(vec):
    max_score = vec[0, argmax(vec)]
    max_score_broadcast = max_score.view(1, -1).expand(1, vec.size()[1])
    return max_score + \
           torch.log(torch.sum(torch.exp(vec - max_score_broadcast)))


class Viterbi:
    def __init__(self, s_to_idx, v_to_idx, tran_matrix, emit_matrix):
        self.s_to_idx = s_to_idx
        self.v_to_idx = v_to_idx
        self.tran_matrix = torch.Tensor(tran_matrix).transpose(0, 1)
        self.emit_matrix = torch.Tensor(emit_matrix).transpose(0, 1)
        self.state_size = len(s_to_idx)

    def viterbi(self, init_state, v_seq):
        backpointers = []
        # 在对数空间初始化维特比变量
        res = []
        init_state = torch.Tensor(init_state)
        for i, s in enumerate(init_state):
            v = self.v_to_idx[v_seq[0]]
            tmp = torch.log(s) + torch.log(self.emit_matrix[v][i])
            res.append(tmp)

        del init_state
        init_vvars = torch.stack(res)

        forward_var = init_vvars
        for v in v_seq[1:]:
            bptrs_t = []
            viterbivars_t = []
            v_index = self.v_to_idx[v]
            for s in range(self.state_size):
                next_tag_var = forward_var + torch.log(self.tran_matrix[s])
                best_tag_id = argmax(next_tag_var)
                bptrs_t.append(best_tag_id)
                viterbivars_t.append(next_tag_var[best_tag_id])
            forward_var = (torch.Tensor(viterbivars_t) + torch.log(self.emit_matrix[v_index]))
            backpointers.append(bptrs_t)
        # 终结
        terminal_var = forward_var
        best_tag_id = argmax(terminal_var)
        path_score = terminal_var[best_tag_id]

        # 回溯解码
        best_path = [best_tag_id]
        for bptrs_t in reversed(backpointers):
            best_tag_id = bptrs_t[best_tag_id]
            best_path.append(best_tag_id)

        best_path.reverse()
        return torch.exp(path_score), best_path


def toIdx(l: List):
    return {e: i for i, e in enumerate(l)}


def main():
    states = ["健康", "发烧"] # tags
    observations = ["正常", "冷", "头晕"]# 
    tran_matrix = torch.Tensor([[0.7, 0.3], [0.4, 0.6]])  # A_ij tagsNum*tagsNum 状态转移矩阵
    emit_matrix = torch.Tensor([[0.5, 0.4, 0.1], [0.1, 0.3, 0.6]]) #tagsNum* obsStates 观测状态矩阵
    init_state = [0.6, 0.4]
    observation_seq = ["正常", "冷", "头晕"]
    viterbi = Viterbi(toIdx(states), toIdx(observations), tran_matrix, emit_matrix)
    maxpro, path = viterbi.viterbi(init_state, observation_seq)
    print("最大概率为：{}".format(maxpro))
    print("最大概率下路径为：")
    pt = ""
    for i in path:
        pt += states[i] + "->"
    print(pt)


main()
```