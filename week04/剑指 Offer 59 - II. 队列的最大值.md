> #### [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

```go
type MaxQueue struct {
	data []int
	//一个单调递减数组
	help []int
}


func Constructor() MaxQueue {
	return MaxQueue{}
}


func (this *MaxQueue) Max_value() int {
	if len(this.help) == 0 {
		return -1
	}
	return this.help[0]
}


func (this *MaxQueue) Push_back(value int)  {
	this.data = append(this.data, value)
	i:=len(this.help)-1
	for i>=0 && value>this.help[i]{
		i--
	}
	this.help = this.help[:i+1]
	this.help = append(this.help, value)
}


func (this *MaxQueue) Pop_front() int {
	if len(this.help) == 0 {
		return -1
	}
	ret := this.data[0]
	if ret == this.help[0] {
		this.help = this.help[1:]
	}
    this.data = this.data[1:]
	return ret
}


/**
 * Your MaxQueue object will be instantiated and called as such:
 * obj := Constructor();
 * param_1 := obj.Max_value();
 * obj.Push_back(value);
 * param_3 := obj.Pop_front();
 */
```

