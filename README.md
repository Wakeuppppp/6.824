# 6.824


```go
	rand.Seed(time.Now().Unix())
	arr := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13}
	slice1 := arr[2:5:5]
	slice2 := arr[1:3:8]
	fmt.Println(len(slice1), cap(slice1)) // 3 3
	fmt.Println(len(slice2), cap(slice2)) // 2 7
```
## 切片扩容策略
Go 中切片扩容的策略是这样的：

如果切片的容量小于 1024 个元素，于是扩容的时候就翻倍增加容量。上面那个例子也验证了这一情况，总容量从原来的4个翻倍到现在的8个。

一旦元素个数超过 1024 个元素，那么增长因子就变成 1.25 ，即每次增加原来容量的四分之一。

注意：扩容扩大的容量都是针对原来的容量而言的，而不是针对原来数组的长度而言的。

## 切片拷贝
在遍历切片的时候, 拿到的value值是值拷贝, 若要修改切片的值, 需要&slice[index]获取真实地址
```go
slice := []int{10, 20, 30, 40}
	for index, value := range slice {
		value += 100 // 修改不起作用, 这里是值拷贝
		slice[index] += 200 
		fmt.Printf("value = %d , value-addr = %x , slice-addr = %x\n", value, &value, &slice[index])
	}
	fmt.Printf("%p\n%v", &slice, slice)
```