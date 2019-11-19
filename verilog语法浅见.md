### 1. “disable” ——跳出循环

* 功能：可以中止任意 **“begin ... ... end ”**  过程块，也可以中止任意**循环语句**（for,repeat等）。
* 下面以代码说明：

```verilog
begin:one
	for(i=1;i<5;i=i+1)
	begin:two
		if(a==0)
			disable one; //从one这个begin..end 中跳出，终止了for
		if(a==1)
			disable two;//从two这个begin..end块中跳出，从本次循环中跳出
	end
end

```

* `disable one`—==相当于 **“break”**== 。因为结束的是“one"这个语句块，**不论"one"这个语句块里执行的是什么语句，都直接跳过**。上述例子中正巧执行的是一个for循环语句，所以相当于提前结束了for循环语句（*换做其他语句，比如always,也会直接跳过*），所以起到了“break”的功能。
* `disable two`—==相当于**“continue"**==。因为”two"这个语句块是在for 循环里面，也就是说，**每次执行完”two"过程块，还没有跳出for循环,要接着回到for的判断语句里接着循环**，所以如果结束的是“two",只是代表**本次循环结束**，但还没有跳出整个 for 循环，所以起到了”continue“的作用。