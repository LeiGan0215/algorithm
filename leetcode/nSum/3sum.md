### 外加一层for循环后，内部退化为一个target-nums[i]的2SUM问题

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++)
        {
            vector<vector<int>> temp;
            TwoSum(temp,nums,i+1,-nums[i]);
            for(vector<int> c:temp)
            {
                c.push_back(nums[i]);
                res.push_back(c);
            }
            while(i<nums.size()-1&&nums[i]==nums[i+1]) i++;
        }
        return res;
    }
    void TwoSum(vector<vector<int>>& res,vector<int> nums,int start,int target)
    {
        int low=start,high=nums.size()-1;
        while(low<high)
        {
            int sum=nums[low]+nums[high];
            int left=nums[low],right=nums[high];
            if(sum==target)
            {
                res.push_back({nums[low],nums[high]});
                while(low<high&&nums[low]==left) low++;
                while(low<high&&nums[high]==right) high--;
            }
            else if(sum<target)
            {
                while(low<high&&nums[low]==left) low++;
            }
            else if(sum>target)
            {
                while(low<high&&nums[high]==right) high--;
            }
        }
    }
};
```

### 双指针法

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        if (nums.size()<3 || nums.back() < 0 || nums.front() > 0) return {};
        for(int t=0;t<nums.size()-2;t++)
        {
            if(nums[t]>0) break;
            if(t>0&&nums[t]==nums[t-1]) continue;
            int left=t+1,right=nums.size()-1;
            while(left<right)
            {
                int p=nums[left]+nums[right]+nums[t];
                if(p==0) 
                {
                    res.push_back({nums[t],nums[left],nums[right]});
                    while(left<right&&nums[right-1]==nums[right]) right--;
                    while(left<right&&nums[left+1]==nums[left]) left++;
                    right--;
                    left++;
                }
                else if(p>0)
                {
                    right--;
                }
                else
                {
                    left++;
                }
            }
        }
        return res;
    }
};
```

