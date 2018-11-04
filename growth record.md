# 个人日常工作采坑成长记录

## 2018-11-03

1. `form`提交时，如果`input`框设置了`disabled`，那么不会提交该`input`框的值。这个以前真没意识到。。。网上说用`readonly`替代，但是我试了下并不符合我的预期，我加了一个`<input type="hidden" name="Data[type]" :value="tupe">`（vue）。

## 2018-11-04

1. `form`默认是`get`提交，我曾经看过，但是真的忘了，还是这两天的一个bug提醒了我。
