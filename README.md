# Name:Iniyasri S
# Register No:212223230081
# 1. Student Attendance Analysis 
A college maintains the daily attendance details of its students in the form of a list containing student IDs. Some students may have attended multiple sessions on the same day. The administration wants to identify the longest continuous sequence of sessions in which no student ID is repeated. Develop a solution that determines the maximum length of such a sequence.
# code
```
arr=list(map(int,input().split()))
seen=set()
left=0
maxlen=0
for right in range(len(arr)):
  while arr[right] in seen:
    seen.remove(arr[left])
    left+=1
  seen.add(arr[right])
  maxlen=max(maxlen,right-left+1)
print(maxlen)
```
# Output
<img width="1607" height="485" alt="image" src="https://github.com/user-attachments/assets/7f20011d-b9a2-4cd4-a447-5a5ba6eaa3e6" />
# 2. Online Shopping Price Analysis
An online shopping application stores the prices of products viewed by a customer during a browsing session. The customer wants to identify a continuous range of products that provides the maximum possible total discount value. Given the discount values, determine the maximum value that can be obtained from any continuous range.
# code
```
arr=list(map(int,input().split()))
curr_sum=0
max_sum=0
for num in arr:
  curr_sum=curr_sum+num
  if curr_sum > max_sum:
    max_sum=curr_sum
  if curr_sum< 0:
    curr_sum=0
print(max_sum)
```
# Output
<img width="1513" height="495" alt="image" src="https://github.com/user-attachments/assets/9a753d98-c651-4796-9668-dfa45717fa84" />

