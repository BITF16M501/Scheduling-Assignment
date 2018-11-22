# Scheduling-Assignment
## First Come First Serve Algorithm in Python

AT=[]
BT=[]
WT=[]
TOT=[]
ST=[]
FT=[]
total_wt=0
total_tt=0
print("Enter total no of processes : ")
n=int(input());
print("Enter Arrival time of processes : ")
AT=list(map(int, input().split()))
print("Enter Burst time of processes : ")
BT=list(map(int, input().split()))
WT.insert(0,0)
ST.insert(0,AT[0])
FT.insert(0,ST[0]+BT[0])
TOT.insert(0,FT[0]-AT[0])
for i in range (1,len(BT)):
	ST.insert(i,FT[i-1])
	FT.insert(i,ST[i]+BT[i])
	TOT.insert(i,FT[i]-AT[i])
	WT.insert(i,ST[i]-AT[i])
	total_wt+=WT[i]
	total_tt+=TOT[i]
print("Processes \t Arrival Time \t Burst Time \t Waiting Time \t Turn Around Time ")
for i in range (0,n):
	print(str(i)+"\t\t " + str(AT[i]) +"\t\t" +str(BT[i]) +"\t\t" +str(WT[i]) +"\t\t" +str(TOT[i]))
avg_wt=float(total_wt)/n
avg_tt=float(total_tt)/n
print("Average waiting time : " +str(avg_wt))
print("Average turn around time : " +str(avg_tt))

## Shortest Job First Algorithm
  
  AT=[]
BT=[]
WT=[]
TOT=[]
ST=[]
FT=[]
total_wt=0
total_tt=0
print("Enter total no of processes : ")
n=int(input());
processes=[]

for i in range (0,n):
	processes.insert(i,i+1)
print("Enter Arrival time of processes : ")
AT=list(map(int, input().split()))
print("Enter Burst time of processes : ")
BT=list(map(int, input().split()))
for i in range(1,n):
	for j in range(1, n-1):
		if BT[j]>BT[j+1]:
			temp=BT[j]
			BT[j]=BT[j+1]
			BT[j+1]=temp
			temp=processes[j]
			processes[j]=processes[j+1]
			processes[j+1]=temp
			temp=AT[j]
			AT[j]=AT[j+1]
			AT[j+1]=temp


WT.insert(0,0)
ST.insert(0,AT[0])
FT.insert(0,ST[0]+BT[0])
TOT.insert(0,FT[0]-AT[0])
for i in range (1,len(BT)):
	ST.insert(i,FT[i-1])
	FT.insert(i,ST[i]+BT[i])
	TOT.insert(i,FT[i]-AT[i])
	WT.insert(i,ST[i]-AT[i])
	total_wt+=WT[i]
	total_tt+=TOT[i]
print("Processes \t Arrival Time \t Burst Time \t Waiting Time \t Turn Around Time ")
for i in range (0,len(BT)):
	print(str(processes[i])+"\t\t " + str(AT[i]) +"\t\t" +str(BT[i]) +"\t\t" +str(WT[i]) +"\t\t" +str(TOT[i]))
avg_wt=float(total_wt)/n
avg_tt=float(total_tt)/n
print("Average waiting time : " +str(avg_wt))
print("Average turn around time : " +str(avg_tt))

## Shortest Remaining Time First 
  
  AT=[]
BT=[]
WT=0
TOT=0
ST=[]
RT=[10]
remain=0
end_time=0
smallest=9
total_wt=0
total_tt=0

print("Enter total no of processes : ")
n=int(input());
print("Enter Arrival time of processes : ")
AT=list(map(int, input().split()))
print("Enter Burst time of processes : ")
BT=list(map(int, input().split()))
for i in range (0,n):
	RT.insert(i,BT[i])
for i in range (n,11):
	RT.insert(i,1000)
a=9
RT.insert(a,9999)

print("Processes \t Arrival Time \t Burst Time \t Completion Time \t Waiting Time \t Turn Around Time ")
t=0

while remain != n :
	smallest=a
	for i in range (0,n):
		if AT[i]<=t and RT[i]< RT[smallest] and RT[i] >0:
			smallest=i	
	
	B=RT[smallest]-1		
	RT.insert(smallest,B)
	print(RT[smallest])
	if RT[smallest] == 0:
		end_time=t+1
		remain=remain+1
		WT=end_time-AT[smallest]-BT[smallest]
		TOT=end_time-AT[smallest]
		print("P"+str(smallest+1)+"\t\t"+str(AT[smallest])+"\t\t"+str(BT[smallest])+"\t\t"+str(end_time)+"\t\t"+str(WT)+"\t\t"+str(TOT))
		total_wt+=WT
		total_tt+=TOT
	t=t+1
avg_wt=float(total_wt)/n
avg_tt=float(total_tt)/n
print("Average waiting time : " +str(avg_wt))
print("Average turn around time : " +str(avg_tt))

## Priority Scheduling Algorithm
  
  AT=[]
BT=[]
WT=[]
TOT=[]
ST=[]
FT=[]
PT=[]
total_wt=0
total_tt=0
print("Enter total no of processes : ")
n=int(input());
processes=[]

for i in range (0,n):
	processes.insert(i,i+1)
print("Enter Arrival time of processes : ")
AT=list(map(int, input().split()))
print("Enter Burst time of processes : ")
BT=list(map(int, input().split()))
print("Enter Priority for each process : ")
PT=list(map(int, input().split()))
for i in range(1,n):
	for j in range(0, i):
		if PT[j]>PT[i] :
			temp=BT[j]
			BT[j]=BT[i]
			BT[i]=temp
			temp=processes[j]
			processes[j]=processes[i]
			processes[i]=temp
			temp=AT[j]
			AT[j]=AT[i]
			AT[i]=temp
WT.insert(0,0)
ST.insert(0,AT[0])
FT.insert(0,ST[0]+BT[0])
TOT.insert(0,FT[0]-AT[0])
for i in range (1,len(BT)):
	ST.insert(i,FT[i-1])
	FT.insert(i,ST[i]+BT[i])
	TOT.insert(i,FT[i]-AT[i])
	WT.insert(i,ST[i]-AT[i])
	total_wt+=WT[i]
	total_tt+=TOT[i]
print("Processes \t Arrival Time \t Burst Time \t Waiting Time \t Turn Around Time ")
for i in range (0,len(BT)):
	print(str(processes[i])+"\t\t " + str(AT[i]) +"\t\t" +str(BT[i]) +"\t\t" +str(WT[i]) +"\t\t" +str(TOT[i]))
avg_wt=float(total_wt)/n
avg_tt=float(total_tt)/n
print("Average waiting time : " +str(avg_wt))
print("Average turn around time : " +str(avg_tt))

## Round Robin Algorithm
  
  AT=[]
BT=[]
RT=[]
WT=[]
TOT=[]
turn_around_time=0
wait_time=0
time_quantum=0
remain=0
time=0
count=0
total_wt=0
total_tt=0
end_time=0
avg_wt=0
avg_tt=0
flag=False
print("Enter total no of processes : ")
n=int(input())
print("Enter Arrival time of processes : ")
AT=list(map(int, input().split()))
print("Enter Burst time of processes : ")
BT=list(map(int, input().split()))
for i in range (0,n):
	RT.insert(i,BT[i])
print("Enter Time quantum : ")
time_quantum=int(input())
print("Processes \t Arrival Time \t Burst Time \t Waiting Time \t Turn Around Time ")
remain=n
i=0
while remain !=0  :
	if RT[count]<=time_quantum and RT[count]>0:
			time+=RT[count]
			RT[count]=0
			flag=True
	elif   RT[count]>0:
		RT[count]-=time_quantum
		time+=time_quantum
	
	if RT[count]==0 and flag==True:
		remain=remain-1
		WT.insert(i,time-AT[count]-BT[count])
		TOT.insert(i,time-AT[count])
		total_wt+=WT[i]
		total_tt+=TOT[i]
		flag=False
		print("P"+str(count+1)+"\t\t"+str(AT[count])+"\t\t"+str(BT[count])+"\t\t"+str(WT[i])+"\t\t"+str(TOT[i])) 
		i+=1
	if count==n-1:
		count=0
	elif AT[count+1]<=time:
		count+=1
	else:
		count=0
avg_wt=float(total_wt)/n
avg_tt=float(total_tt)/n
print("Average waiting time : " +str(avg_wt))
print("Average turn around time : " +str(avg_tt))

## Multi Level Queue
  
  AT=[]
BT=[]
WT=[]
TOT=[]
ST=[]
FT=[]
PT=[]
total_wt=0
total_tt=0
print("Enter total no of processes : ")
n=int(input());
processes=[]

for i in range (0,n):
	processes.insert(i,i+1)
print("Enter Arrival time of processes : ")
AT=list(map(int, input().split()))
print("Enter Burst time of processes : ")
BT=list(map(int, input().split()))
print("Enter Priority for Processes (system/user) (system=0,user=1) : ")
PT=list(map(int, input().split()))
for i in range(1,n):
	for j in range(0, i):
		if PT[j]>PT[i]:
			temp=BT[j]
			BT[j]=BT[i]
			BT[i]=temp
			temp=processes[j]
			processes[j]=processes[i]
			processes[i]=temp
			temp=AT[j]
			AT[j]=AT[i]
			AT[i]=temp
			
			
WT.insert(0,0)
ST.insert(0,AT[0])
FT.insert(0,ST[0]+BT[0])
TOT.insert(0,FT[0]-AT[0])
for i in range (1,len(BT)):
	ST.insert(i,FT[i-1])
	FT.insert(i,ST[i]+BT[i])
	TOT.insert(i,FT[i]-AT[i])
	WT.insert(i,ST[i]-AT[i])
	total_wt+=WT[i]
	total_tt+=TOT[i]
print("Processes \t Arrival Time \t Burst Time \t Waiting Time \t Turn Around Time ")
for i in range (0,len(BT)):
	print(str(processes[i])+"\t\t " + str(AT[i]) +"\t\t" +str(BT[i])+"\t\t" +str(WT[i]) +"\t\t" +str(TOT[i]))
avg_wt=float(total_wt)/n
avg_tt=float(total_tt)/n
print("Average waiting time : " +str(avg_wt))
print("Average turn around time : " +str(avg_tt))

	
  
  
