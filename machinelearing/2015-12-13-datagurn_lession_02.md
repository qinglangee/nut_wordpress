# ml 第二课

多重共线性 （ML02f.mp4 30分钟左右）

看 最大特征根与最小特征根比值， kappa
R 函数

	kappa(z, exact = FALSE, ...)


	collinear <-data.frame(
		Y=c(1,2,3,4,5,6,7,8,9,10,11,12),
		X1=rep(c(1,2,3,4), c(1，2，3，4)),
		X2=rep(c(1,2,3), c(1,2,3)),
		X3=c(1,2,3,4,5,6,7,8,9,10,11,12)
	)
	XX<-cor(collinear[2:7])
	kappa(XX, exact=TRUE)

	// 找出哪些变量是多重共线性
	eigen(XX)  

> iris.a4=lm(Sepal.Length～Sepal.Width, data=iris)
> iris.a4
错误: 找不到对象'iris.a4'