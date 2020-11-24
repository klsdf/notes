主要是借助java的集合进行排序和各种处理。让每次优先级最大的进程被处理。

```java
package 测试;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;


public class Process {
	enum PROCESS_STATE {
		ready
	}

	/**
	 * PCB类是专门用来记录进程信息的<br/>
	 * ID 进程标识数<br/>
	 * PRIORITY 进程优先数：优先数越大，优先级越高<br/>
	 * CPUTIME 进程已占用时间片：每得到一次调度，值加1；<br/>
	 * ALLTIME 进程还需占用时间片：每得到一次调度，该值减1，一旦运行完毕，ALLTIME为0<br/>
	 * NEXT 进程队列指针：用来将PCB排成队列<br/>
	 * STATE 进程状态：一般为就绪，可以不用
	 * 
	 * @author 闫辰祥
	 * 
	 */
	class PCB implements Comparable<PCB> {
		int ID;
		int PRIORITY;
		int CPUTIME;
		int ALLTIME;
		PCB NEXT;
		PROCESS_STATE STATE;

		public PCB(int id, int priority, int cputime, int alltime, PCB next) {
			ID = id;
			PRIORITY = priority;
			CPUTIME = cputime;
			ALLTIME = alltime;
			NEXT = next;
			STATE = PROCESS_STATE.ready;
		}

		public PCB(int id, int priority, int cputime, int alltime) {
			ID = id;
			PRIORITY = priority;
			CPUTIME = cputime;
			ALLTIME = alltime;
			NEXT = null;
			STATE = PROCESS_STATE.ready;
		}

		@Override
		public int compareTo(PCB p) {
			return p.PRIORITY - this.PRIORITY;
		}
		
	}
	public static void run(List<PCB> PCBList) {
		while(PCBList.size()!=0){
			Collections.sort(PCBList);
			PCB nowProcess = PCBList.get(0);
			
			System.out.println("当前正在运行的进程："+nowProcess.ID);
			System.out.print("当前就绪队列：");
			for (int i = 1; i < PCBList.size(); i++) {
				System.out.print(PCBList.get(i).ID+" ");
			}
			System.out.println("\n");
			
			
			nowProcess.CPUTIME+=1;
			nowProcess.ALLTIME-=1;
			nowProcess.PRIORITY-=3;
			if(nowProcess.ALLTIME==0)
				PCBList.remove(0);
		}
	}
	

	public static void main(String[] args) {
		List<PCB> PCBList = new ArrayList<PCB>();
		PCBList.add(new Process().new PCB(0, 9, 0, 3));
		PCBList.add(new Process().new PCB(1, 38, 0, 2));
		PCBList.add(new Process().new PCB(2, 30, 0, 6));
		PCBList.add(new Process().new PCB(3, 29, 0, 3));
		PCBList.add(new Process().new PCB(4, 0, 0, 4));
		
		run(PCBList);
	}
}
```

