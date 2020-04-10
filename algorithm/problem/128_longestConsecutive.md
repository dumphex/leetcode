# [最长连续序列]()

```

```

# Solution

## solution1: 超时
```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        if (nums.empty()) {
            return 0;
        }

        std::unordered_map<int, int> map;
        int max = 0;

        for(auto n : nums) {
            if (map.find(n) != map.end()) {
                continue;
            }

            if (map.find(n - 1) == map.end()) {
                map[n] = 1;
            } else {
                map[n] = map[n - 1] + 1;
            }
                
            max = std::max(max, map[n]);

            while(map.find(++n) != map.end()) {
                map[n] = map[n - 1] + 1;
                max = std::max(max, map[n]);
            }
        }

        return max;
    }
};
```

## solution2: 
```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        if (nums.empty()) {
            return 0;
        }

        std::unordered_set<int> set;
        for(auto n : nums) {
            set.insert(n);
        }

        int max = 0;
        for(auto n : nums) {
            if (set.find(n - 1) == set.end()) {
                int counter = 1;
                while(set.find(++n) != set.end()) {
                    counter++;
                }
                max = std::max(max, counter);
            } 
        }

        return max;
    }
};
```
