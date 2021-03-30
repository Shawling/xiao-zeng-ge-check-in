> #### [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

```go
func maxSlidingWindow(nums []int, k int) []int {
	if len(nums) == 0 && k == 0 {
		return []int{}
	}
	//单调递减数组
	decrease := make([]int, k)
	for i := range decrease {
		decrease[i] = -math.MaxInt64
	}
	ret := make([]int, len(nums)-k+1)
	for i, n := range nums {
		//如果是前k-1个，不出队，不计算最大值
		if i<k-1 {
			decreasify(&decrease, n)
			continue
		}
		//出队
		if i>=k && decrease[0] == nums[i-k] {
			decrease = decrease[1:]
		}
		decreasify(&decrease, n)
		ret[i-k+1] = decrease[0]
	}
	return ret
}

func decreasify(decrease *[]int, value int){
	i:=len(*decrease)-1
	//找到value的位置
	for i>=0 && value>(*decrease)[i]{
		i--
	}
	*decrease = (*decrease)[:i+1]
	*decrease = append(*decrease, value)
}
```

