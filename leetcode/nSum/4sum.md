```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++)
        {
            vector<vector<int>> temp;
            ThreeSum(temp,nums,i+1,target-nums[i]);
            for(vector<int> c:temp)
            {
                c.push_back(nums[i]);
                res.push_back(c);
            }
            while(i<nums.size()-1&&nums[i]==nums[i+1]) i++;
        }
        return res;
    }
    void ThreeSum(vector<vector<int>>& res,vector<int> nums,int start,int target)
    {
        for(int i=start;i<nums.size();i++)
        {
            vector<vector<int>> temp;
            TwoSum(temp,nums,i+1,target-nums[i]);
            for(vector<int> c:temp)
            {
                c.push_back(nums[i]);
                res.push_back(c);
            }
            while(i<nums.size()-1&&nums[i]==nums[i+1]) i++;
        }
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
            else if(sum>target)
            {
                while(low<high&&nums[high]==right) high--;
            }
            else if(sum<target)
            {
                while(low<high&&nums[low]==left) low++;
            }
        }
    }
};
```

