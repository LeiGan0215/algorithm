### 哈希表

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> data;
        for(int i=0;i<nums.size();i++)
        {
            if(data.count(target-nums[i]))
                return {i,data[target-nums[i]]};
            data[nums[i]]=i;
        }
        return {};
    }
};
```

### 双指针

```c++
class Solution {
public:
    static vector<int>* nums_ptr;
    static bool cmp(int left,int right)
    {
        return (*nums_ptr)[left]<(*nums_ptr)[right];
    }
    vector<int> twoSum(vector<int>& nums, int target) {
        nums_ptr=&nums;
        vector<int> index(nums.size(),0);
        for(int i=0;i<nums.size();i++)
            index[i]=i;
        sort(index.begin(),index.end(),Solution::cmp);
        int low=0,high=nums.size()-1;
        while(low<high)
        {
            int sum=nums[index[low]]+nums[index[high]];
            if(sum==target)
            {
                return {index[low],index[high]};
            }
            else if(sum<target)
                low++;
            else if(sum>target)
                high--;
        }
        return {};
    }
};
vector<int> * Solution::nums_ptr = NULL;
```

