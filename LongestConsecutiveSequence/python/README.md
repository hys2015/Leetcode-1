**思路**

思路一: 通过 dict(哈希表) 去实现:
遍历列表,假设字典为 hash_dict, 列表为 nums, 元素为 num, 最大长度 max_len = 0,如果 num 不在字典中,判断 num - 1, num + 1 是否 hash_dict 中,对应值分别为 left, right, 不在则值为 0, 然后获取累加值 cur_len = 1 + left + right,然后取 max_len 和 cur_len 的最大值, 然后将 cur_len 依次赋值给 hash_dict[num],hash_dict[num-1],dict[num+1]


思路二: 直接遍历列表:
遍历列表,假设列表为 nums, 先用 set 去重,得到新的 nums,元素为 num,最大长度为 max_len = 0, 当前长度为 cur_len, 首先 num 肯定在 nums 中,然后判断 num+1 是否在 nums, ... , nums + N 是否在 nums 中, 然后判断 max_len 和 cur_len 的长度,取最大值,为了防止重复遍历数组,我们在循环前,先判断 num -1 是否在 nums 中,如果在,就说明存在 num - 1 进行了循环
 
**解法**


解法一

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        hash_dict = {}
        max_len = 0
        for num in nums:
            if num not in hash_dict:
                left = hash_dict.get(num-1,0)
                right = hash_dict.get(num+1,0)
                cur_len = 1 + left + right
                max_len = max(max_len, cur_len)
                hash_dict[num] = cur_len
                hash_dict[num - left] = cur_len
                hash_dict[num + right] = cur_len
        return max_len
```

解法二 

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        max_len = 0
        nums = set(nums)
        for num in nums:
            if num -1  not in nums:
                current_num = num
                current_len = 1
                while current_num + 1 in nums:
                    current_len += 1
                    current_num += 1
                max_len = max(max_len,current_len)     
        return max_len
```