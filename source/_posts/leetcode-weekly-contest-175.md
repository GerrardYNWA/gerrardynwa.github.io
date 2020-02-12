title: LeetCode Weekly Contest 175
date: 2020-02-12 15:08:15
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第175场周赛

<!-- more -->

## 1. [Check If N and Its Double Exist](https://leetcode.com/contest/weekly-contest-175/problems/check-if-n-and-its-double-exist/)

```C++
class Solution {
public:
    bool checkIfExist(vector<int>& arr) {
        int zero = 0;
        unordered_set<int> st;
        for (int a : arr) {
            if (a == 0) zero++;
            st.insert(a);
        }
        
        if (zero >= 2) return true;
        
        for (int a : arr) {
            if (a != 0 && st.find(2 * a) != st.end()) return true;
        }
        
        return false;
    }
};
```

## 2. [Minimum Number of Steps to Make Two Strings Anagram](https://leetcode.com/contest/weekly-contest-175/problems/minimum-number-of-steps-to-make-two-strings-anagram/)

```C++
class Solution {
public:
    int minSteps(string s, string t) {
        vector<int> mp(26, 0);
        for (char c : s) {
            mp[c - 'a']++;
        }
        
        for (char c : t) {
            mp[c - 'a']--;
        }
        
        int ans = 0;
        for (int i = 0; i < 26; i++) {
            if (mp[i] > 0) ans += mp[i];
        }
        
        return ans;
    }
};
```

## 3. [Tweet Counts Per Frequency](https://leetcode.com/contest/weekly-contest-175/problems/tweet-counts-per-frequency/)

```C++
class TweetCounts {
public:
    unordered_map<string, vector<int>> mp;
    
    int getSecond(string s) {
        if (s == "minute") return 60;
        else if (s == "hour") return 3600;
        else return 86400;
    }
    
    TweetCounts() {
        unordered_map<string, vector<int>> tmp;
        mp.swap(tmp);
    }
    
    void recordTweet(string tweetName, int time) {
        mp[tweetName].push_back(time);
    }
    
    vector<int> getTweetCountsPerFrequency(string freq, string tweetName, int startTime, int endTime) {
        int f = getSecond(freq);
        int k = (endTime - startTime) / f + 1;
        vector<int> result(k, 0);
        vector<int> times = mp[tweetName];
        
        for (int i = 0; i < times.size(); i++) {
            if (times[i] >= startTime && times[i] <= endTime) {
                int t = (times[i] - startTime) / f;
                result[t]++;
            } 
        }
        
        return result;
    }
};

/**
 * Your TweetCounts object will be instantiated and called as such:
 * TweetCounts* obj = new TweetCounts();
 * obj->recordTweet(tweetName,time);
 * vector<int> param_2 = obj->getTweetCountsPerFrequency(freq,tweetName,startTime,endTime);
 */
```

## 4. [Maximum Students Taking Exam](https://leetcode.com/contest/weekly-contest-175/problems/maximum-students-taking-exam/)

```C++

```

