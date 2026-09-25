# Problem_analysis
## Name : Iniyasri S
## Reg no : 212223230081
**1. Student Attendance Analysis
A college maintains the daily attendance details of its students in the form of a list containing student IDs. Some students may have attended multiple sessions on the same day. The administration wants to identify the longest continuous sequence of sessions in which no student ID is repeated. Develop a solution that determines the maximum length of such a sequence.**
```
def longest_unique_attendance(ids):
    seen = set()
    left = 0
    max_len = 0
    
    for right in range(len(ids)):
        while ids[right] in seen:
            seen.remove(ids[left])
            left += 1
        seen.add(ids[right])
        max_len = max(max_len, right - left + 1)
    
    return max_len
print(longest_unique_attendance(['A','B','C','A','D','E','F']))
```
```
def longest_unique_attendance_map(ids):
    last_index = {}
    left = 0
    max_len = 0
    
    for right, student in enumerate(ids):
        if student in last_index and last_index[student] >= left:
            left = last_index[student] + 1
        last_index[student] = right
        max_len = max(max_len, right - left + 1)
    
    return max_len
print(longest_unique_attendance_map(['A','B','C','A','D','E','F']))
```
# Output
<img width="990" height="698" alt="image" src="https://github.com/user-attachments/assets/d5f18b38-9561-4063-ad9f-ef53ff16e769" />

**2.Online Shopping Price Analysis
An online shopping application stores the prices of products viewed by a customer during a browsing session. The customer wants to identify a continuous range of products that provides the maximum possible total discount value. Given the discount values, determine the maximum value that can be obtained from any continuous range.**

```
def max_discount(values):
    max_sum = values[0]
    current_sum = values[0]
    
    for v in values[1:]:
        current_sum = max(v, current_sum + v)
        max_sum = max(max_sum, current_sum)
    
    return max_sum
print(max_discount([-2, 1, -3, 4, -1, 2, -2, -5, 4]))
```
```
def max_discount_dc(values):
    def helper(l, r):
        if l == r:
            return values[l]
        mid = (l + r) // 2
        left_max = helper(l, mid)
        right_max = helper(mid + 1, r)
        curr = 0
        left_cross = float('-inf')
        for i in range(mid, l - 1, -1):
            curr += values[i]
            left_cross = max(left_cross, curr)
        curr = 0
        right_cross = float('-inf')
        for i in range(mid + 1, r + 1):
            curr += values[i]
            right_cross = max(right_cross, curr)
        
        return max(left_max, right_max, left_cross + right_cross)
    
    return helper(0, len(values) - 1)
print(max_discount_dc([-2, 1, -3, 4, -1, 2, 1, -5, 4]))
```
# Output 
<img width="1025" height="725" alt="image" src="https://github.com/user-attachments/assets/5bb89042-c389-4ddd-a194-eb7939ceabed" />


**3. Rainwater Collection System
A city installs buildings of different heights along a straight road. During rainfall, water gets collected between taller buildings. The engineering team needs to calculate the total amount of water that can remain trapped after heavy rainfall based on the heights of the buildings**
```
def trap_prefix(height):
    if not height:
        return 0
    n = len(height)
    
    left_max = [0] * n
    right_max = [0] * n
    
    left_max[0] = height[0]
    for i in range(1, n):
        left_max[i] = max(left_max[i-1], height[i])
    
    right_max[n-1] = height[n-1]
    for i in range(n-2, -1, -1):
        right_max[i] = max(right_max[i+1], height[i])
    
    water = 0
    for i in range(n):
        water += min(left_max[i], right_max[i]) - height[i]
    
    return water
print(trap_prefix([3, 0, 2, 0, 4])) 
print(trap_prefix([0,1,0,2,1,0,1,3,2,1,2,1]))
```
```
def trap_two_pointers(height):
    if not height:
        return 0
    
    left, right = 0, len(height) - 1
    left_max, right_max = 0, 0
    water = 0
    
    while left < right:
        if height[left] < height[right]:
            if height[left] >= left_max:
                left_max = height[left]
            else:
                water += left_max - height[left]
            left += 1
        else:
            if height[right] >= right_max:
                right_max = height[right]
            else:
                water += right_max - height[right]
            right -= 1
    
    return water
print(trap_two_pointers([3, 0, 1, 0, 4])) 
print(trap_two_pointers([0,1,0,2,1,0,1,3,2,4,2,1])) 
```

# Output
<img width="1247" height="627" alt="image" src="https://github.com/user-attachments/assets/839406c5-b91a-4da0-97ca-926949f1478c" />
<img width="1001" height="673" alt="image" src="https://github.com/user-attachments/assets/f8665eb6-6bd2-4c3c-8b7d-73015fd461b1" />


**4. Employee Performance Analysis
A company stores the monthly performance scores of an employee for several months. The scores may contain both positive and negative values depending on the employee's performance. Management wants to identify the continuous period during which the employee achieved the highest overall performance**
```
def best_performance(scores):
    max_sum = scores[0]
    current = scores[0]
    
    for s in scores[1:]:
        current = max(s, current + s)
        max_sum = max(max_sum, current)
    
    return max_sum
print(best_performance([-1, 3, -5, 5, -1]))
```
```
def best_performance_dp(scores):
    n = len(scores)
    dp = [0] * n
    dp[0] = scores[0]
    
    for i in range(1, n):
        dp[i] = max(scores[i], dp[i-1] + scores[i])
    
    return max(dp)
print(best_performance_dp([-1, 3, -2, 8, -1]))
```
# Output
<img width="1378" height="617" alt="image" src="https://github.com/user-attachments/assets/c695fd9b-ae6c-4da1-8c9d-b74ef9a79d81" />

**5. Product Sales Analysis
A retail company stores the daily sales quantity of a product for several consecutive days. Due to seasonal changes, some days may have negative adjustments. The company wants to identify the period that produced the highest multiplication of sales-related values. Develop a solution to determine this maximum product**
```
def max_sales_product(nums):
    if not nums:
        return 0
    
    max_prod = min_prod = result = nums[0]
    
    for n in nums[1:]:
        if n < 0:
            max_prod, min_prod = min_prod, max_prod
        max_prod = max(n, max_prod * n)
        min_prod = min(n, min_prod * n)
        result = max(result, max_prod)
    
    return result
print(max_sales_product([2, 3, -2, 4]))
print(max_sales_product([-2, 0, -1]))
```
```
def max_sales_product_brute(nums):
    if not nums:
        return 0
    
    result = nums[0]
    for i in range(len(nums)):
        prod = 1
        for j in range(i, len(nums)):
            prod *= nums[j]
            result = max(result, prod)
    
    return result
print(max_sales_product_brute([2, 3, -2, 4]))
```
# Output
<img width="678" height="456" alt="image" src="https://github.com/user-attachments/assets/559ed9df-77c1-49b1-a67a-d279bf27e1df" />

<img width="863" height="366" alt="image" src="https://github.com/user-attachments/assets/629491aa-a7b0-4ca0-aa89-bcb30967b8d3" />


**6. Customer Purchase History
An e-commerce application stores the product IDs purchased by a customer in chronological order. The same product may appear multiple times. The system needs to determine the longest sequence of consecutive purchases in which every product ID is unique**
```
def longest_unique_purchases(purchases):
    last_seen = {}
    left = 0
    max_len = 0
    
    for right, pid in enumerate(purchases):
        if pid in last_seen and last_seen[pid] >= left:
            left = last_seen[pid] + 1
        last_seen[pid] = right
        max_len = max(max_len, right - left + 1)
    
    return max_len
print(longest_unique_purchases([1, 2, 1, 3, 4]))
```
# output
<img width="763" height="367" alt="image" src="https://github.com/user-attachments/assets/d80f909e-6614-4931-bba8-7f9b72098df4" />

**7. Bank Transaction Analysis
A bank stores transaction amounts for a customer's account. A continuous group of transactions may add up to a specific target amount. The auditing system needs to determine how many different continuous transaction groups produce exactly the specified amount**
```
def count_subarrays_sum_k(transactions, target):
    prefix_count = {0: 1}
    prefix_sum = 0
    count = 0
    
    for t in transactions:
        prefix_sum += t
        if prefix_sum - target in prefix_count:
            count += prefix_count[prefix_sum - target]
        prefix_count[prefix_sum] = prefix_count.get(prefix_sum, 0) + 1
    
    return count
print(count_subarrays_sum_k([1, 2, 3, -2, 5], 3))
```
```
def count_subarrays_sum_k_brute(transactions, target):
    count = 0
    n = len(transactions)
    
    for i in range(n):
        total = 0
        for j in range(i, n):
            total += transactions[j]
            if total == target:
                count += 1
    
    return count
print(count_subarrays_sum_k_brute([1, 2, 3, -2, 5], 3))
```
# Output
<img width="805" height="686" alt="image" src="https://github.com/user-attachments/assets/6fcea1f7-89e7-42cf-95f6-8abad1dc91ad" />

**8.8. Employee Skill Grouping
A company receives a list of employee skill codes represented as strings. Employees having the same set of characters in their skill codes belong to the same skill category, even if the characters appear in a different order. The HR system needs to organize employees into appropriate skill groups**
```
def group_skills(codes):
    groups = {}
    
    for code in codes:
        key = ''.join(sorted(code))
        groups.setdefault(key, []).append(code)
    
    return list(groups.values())
print(group_skills(["abc", "bca", "cab", "xyz", "zyx"]))
```
# Output
<img width="781" height="243" alt="image" src="https://github.com/user-attachments/assets/eba41794-addf-4aad-8ef6-44a30ba02299" />

**9.A network monitoring system receives packet identifiers in chronological order. The system must determine the longest sequence of consecutive packets whose identifiers form a continuous numerical sequence, regardless of their original order in the incoming data.**
```
def longest_consecutive_packets_sort(packets):
    if not packets:
        return 0
    
    nums = sorted(set(packets))
    longest = 1
    current = 1
    
    for i in range(1, len(nums)):
        if nums[i] == nums[i-1] + 1:
            current += 1
        else:
            current = 1
        longest = max(longest, current)
    
    return longest
print(longest_consecutive_packets_sort([100, 4, 200, 1, 3, 2]))
```
# Output
<img width="812" height="452" alt="image" src="https://github.com/user-attachments/assets/a20da2d1-2daa-45df-a2aa-596b734c6e79" />

**10.A hospital receives appointment requests represented by starting and ending times. Some appointments overlap with each other. The scheduling system needs to combine overlapping appointment periods so that the final schedule contains only non-overlapping time ranges.**
```
def merge_appointments(intervals):
    if not intervals:
        return []
    
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    
    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    
    return merged
print(merge_appointments([[1,3],[2,6],[8,10],[15,18]]))
```
```
def merge_appointments_sweep(intervals):
    events = []
    for s, e in intervals:
        events.append((s, 1))   # start
        events.append((e, -1))  # end
    events.sort()
    
    result = []
    active = 0
    start = None
    
    for time, typ in events:
        if active == 0:
            start = time
        active += typ
        if active == 0:
            result.append([start, time])
    
    return result
print(merge_appointments_sweep([[1,3],[2,6],[8,10],[15,18]]))
```
# Output
<img width="896" height="372" alt="image" src="https://github.com/user-attachments/assets/78b09ced-1da8-4805-941c-ec694f0a2b0a" />

<img width="976" height="485" alt="image" src="https://github.com/user-attachments/assets/22c46484-5697-4bd1-826c-137d4e9dbd01" />
