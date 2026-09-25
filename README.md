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
max_sum=arr[0]
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

# 3. Rainwater Collection System
A city installs buildings of different heights along a straight road. During rainfall, water gets collected between taller buildings. The engineering team needs to calculate the total amount of water that can remain trapped after heavy rainfall based on the heights of the buildings
# code
```
height=list(map(int,input().split()))
left=0
right=len(height)-1
max_wat=0
while left<right:
  width=right-left
  h=min(height[left],height[right])
  curr_wat=width*h
  max_wat=max(curr_wat,max_wat)
  if height[left]<height[right]:
    left+=1
  else:
    right-=1
print(max_wat)
```
# Output
<img width="1096" height="582" alt="image" src="https://github.com/user-attachments/assets/352f6c25-4039-4db1-9fcf-fec7767c4507" />
# 4. Employee Performance Analysis
A company stores the monthly performance scores of an employee for several months. The scores may contain both positive and negative values depending on the employee's performance. Management wants to identify the continuous period during which the employee achieved the highest overall performance
# code
```
arr=list(map(int,input().split()))
curr_sum=0
max_sum=arr[0]
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
# 5. Product Sales Analysis
A retail company stores the daily sales quantity of a product for several consecutive days. Due to seasonal changes, some days may have negative adjustments. The company wants to identify the period that produced the highest multiplication of sales-related values. Develop a solution to determine this maximum product.
# code
```
def max_sales_product(sales):
    if not sales:
        return 0

    max_prod = sales[0]
    min_prod = sales[0]
    result = sales[0]

    for i in range(1, len(sales)):
        curr = sales[i]
        
        if curr < 0:
            max_prod, min_prod = min_prod, max_prod

        max_prod = max(curr, max_prod * curr)
        min_prod = min(curr, min_prod * curr)

        result = max(result, max_prod)

    return result


sales = list(map(int, input().split()))


print(max_sales_product(sales))
```
# Output
<img width="1125" height="632" alt="image" src="https://github.com/user-attachments/assets/37105d39-2d7f-4bc3-b63c-247b4ee4a45c" />

# 6. Customer Purchase History
An e-commerce application stores the product IDs purchased by a customer in chronological order. The same product may appear multiple times. The system needs to determine the longest sequence of consecutive purchases in which every product ID is unique.

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
# 7. Bank Transaction Analysis
A bank stores transaction amounts for a customer's account. A continuous group of transactions may add up to a specific target amount. The auditing system needs to determine how many different continuous transaction groups produce exactly the specified amount.
# code
```
def count_transaction_groups(transactions, target):
    prefix_sums = {0: 1}
    current_sum = 0
    count = 0

    for amount in transactions:
        current_sum += amount
        if (current_sum - target) in prefix_sums:
            count += prefix_sums[current_sum - target]
        prefix_sums[current_sum] = prefix_sums.get(current_sum, 0) + 1

    return count

transactions = [10, 20, -10, 30, -20, 10]
target = 20
print(f"Continuous transaction groups count: {count_transaction_groups(transactions, target)}")
```
# Output
<img width="1425" height="557" alt="image" src="https://github.com/user-attachments/assets/c0cd4f27-2721-4567-8a28-e5308011f3ca" />
# 8. Employee Skill Grouping
A company receives a list of employee skill codes represented as strings. Employees having the same set of characters in their skill codes belong to the same skill category, even if the characters appear in a different order. The HR system needs to organize employees into appropriate skill groups.
# code
```
from collections import defaultdict

def group_employee_skills(skill_codes):
    grouped_skills = defaultdict(list)

    for code in skill_codes:
        sorted_key = "".join(sorted(code))
        grouped_skills[sorted_key].append(code)

    return list(grouped_skills.values())

skill_codes = ["python", "typhon", "java", "aavj", "c++"]
print("Skill groups:", group_employee_skills(skill_codes))
```
# Output

<img width="1600" height="442" alt="image" src="https://github.com/user-attachments/assets/c4d70693-9328-4fdd-a286-35ee55b9c8f8" />

# 9. Network Packet Analysis
A network monitoring system receives packet identifiers in chronological order. The system must determine the longest sequence of consecutive packets whose identifiers form a continuous numerical sequence, regardless of their original order in the incoming data
# code
```
def longest_packet_sequence(packet_ids):
    id_set = set(packet_ids)
    longest_streak = 0

    for packet in id_set:
        # Check if it's the start of a sequence
        if packet - 1 not in id_set:
            current_packet = packet
            current_streak = 1

            while current_packet + 1 in id_set:
                current_packet += 1
                current_streak += 1

            longest_streak = max(longest_streak, current_streak)

    return longest_streak

packet_ids = [100, 4, 200, 1, 3, 2]
print(f"Longest continuous sequence length: {longest_packet_sequence(packet_ids)}")
```
# Output

<img width="1357" height="577" alt="image" src="https://github.com/user-attachments/assets/d864b792-ba53-4f2d-b2d8-22dd31313767" />

# 10. Hospital Appointment Scheduling
A hospital receives appointment requests represented by starting and ending times. Some appointments overlap with each other. The scheduling system needs to combine overlapping appointment periods so that the final schedule contains only non-overlapping time ranges
# code
```
def merge_appointments(appointments):
    if not appointments:
        return []
    appointments.sort(key=lambda x: x[0])
    merged = [appointments[0]]

    for start, end in appointments[1:]:
        prev_start, prev_end = merged[-1]

        if start <= prev_end:
            merged[-1] = (prev_start, max(prev_end, end))
        else:
            merged.append((start, end))

    return merged

appointments = [(9, 11.5), (10, 12), (13, 15), (14, 16.5)]
merged_schedule = merge_appointments(appointments)

print("Final Schedule (Non-Overlapping Time Ranges):")
for start, end in merged_schedule:
    print(f"Appointment Slot: {start} to {end}")

```
# Output

<img width="1387" height="615" alt="image" src="https://github.com/user-attachments/assets/e708a269-c148-4725-981b-30c09ae1a757" />



