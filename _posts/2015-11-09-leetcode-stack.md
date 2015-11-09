---
layout: post
title: LeetCode stack problem
categories: [Code]
tags: [LeetCode]
description: LeetCode 堆栈问题
comments: true
---
* TOC
{:toc}   

##第一题 [逆波兰表达式][1]

> Evaluate the value of an arithmetic expression in Reverse Polish Notation.
>
>Valid operators are +, -, *, /. Each operand may be an integer or another expression.
>
>Some examples:
>
>
>
	  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
      ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6

**解答：**
{% highlight cpp %}
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
    	if(tokens.empty()) return 0;
        stack<string> s;
        int first, second;
        for(int i = 0; i < tokens.size(); i++) {
        	if (tokens[i] != "+" && tokens[i] != "-" && tokens[i] != "*" && tokens[i] != "/")
            	s.push(tokens[i]);
            else {
            	second = atoi(s.top().c_str());
                s.pop();
            	first = atoi(s.top().c_str());
                s.pop();
                if (tokens[i] == "+") {
                	s.push(to_string(first + second));
                } else if (tokens[i] == "-") {
                	s.push(to_string(first - second));
                } else if (tokens[i] == "*") {
                	s.push(to_string(first * second));
                } else if (tokens[i] == "/") {
                	s.push(to_string(first / second));
                }
            }
        }
        return atoi(s.top().c_str());
    }
};
{% endhighlight %}

##第二题[最长有效匹配括号子串][2]

>Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

>For "(()", the longest valid parentheses substring is "()", which has length = 2.

>Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.


**解答**
从右往左，一维数组动态规划，dp[i]代表当前点(必须包含当前点)到最后一点的最长匹配
{% highlight cpp %}
class Solution {
public:
    int longestValidParentheses(string s) {
        int maxLen = 0;
        int dp[65536];
        int size = s.size();
        for (int j = 0; j < size; ++j) 
            dp[j] = 0;
        for (int i = size - 2; i >= 0; --i) {
            if (s[i] == '(') {
                if (i + dp[i+1] + 1 <= size - 1)
                {
                    if (s[i+dp[i+1]+1] == ')') {
                        dp[i] = dp[i+1]+2;
                        if (i + dp[i+1] + 1 < size - 1)
                            dp[i] += dp[i+dp[i+1] + 2];
                        maxLen = max(maxLen, dp[i]);
                    }
                }
            }
        }

        return maxLen;
    }
};
{% endhighlight %}

[1]:https://leetcode.com/problems/evaluate-reverse-polish-notation/
[2]:https://leetcode.com/problems/longest-valid-parentheses/
