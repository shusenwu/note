```
题目二： 组建球队， 给一个list 是每个人的socres, 还有一个list 是每个人的ages，
同一个球队里面， 没有人数限制， 但是年长的人的score必须大于年少的人的score， 这俩人才能在一个队
age2>age1 =>  score2>score1
返回队伍的最大score
eg. scores = [4, 5, 6, 5] ages = [2, 1, 2, 1]

先根据年龄排序，然后对成绩维持一个monotonic queue 保持递增或者相等（非递减），然后每次在queue里面取max 的sum 
```
