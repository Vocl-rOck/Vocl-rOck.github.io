#operating system_4th
>信息量
>经典同步问题：生产者-消费者问题

## 信息量
>所有进程共享信息量
>根据取值来调用资源
>只有操作系统才可以改变信息量

+ **描述一个系统资源占用情况的数据结构**
	+ **当信息量的值>=0时，代表空闲资源的数量**
	+ **当信息量的值<0时，代表因为该资源的阻塞队列中进程的数量**
信息量数据结构定义：

 `struct semaphore{`
 `int value;`
 `struct semaphore *queue`
 `}semaphore;`

## 应用信息量来实现进程同步和互斥 
两个操作原语来改变信息量
>p操作：向系统申请一个单位的资源
>v操作：向系统释放一个单位的资源，v原语通常还意味着唤醒进程等待队列中的头一个进程
>mute表示初始为1的信息量，以实现互斥
**p（mute）**
	*临界区代码*（<font color=#00ffff size=3>进程中访问临界资源的一段代码</font>）
**v（mute）**
	*剩下的语句*

	p(s)
	{s.value--;
	if(s.value<0)
	block(s.queue)
	}

    v(s)
    {
	    s.value++;
	    if(s.value<=0)
		    wakeup(s.queue);
    }
***
##经典互斥同步问题
>生产者-消费者问题

+ 一个生产者和一个消费者及一个缓冲区资源
    

		pi{
			while(ture)
			{
			
			p(mute);
			//临界区代码
			v(mute);
				remainder section i;//这个remainder section有啥用
			}
	+ 一个生产者和一个消费者及多个缓冲区资源
		    >生产者和消费者互斥
			>缓冲区并行
		
		


 
