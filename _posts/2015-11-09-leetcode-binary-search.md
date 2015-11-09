---
layout: post
title: LeetCode binary search problem
categories: [Code]
tags: [LeetCode]
description: LeetCode 二分搜索问题
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
{% highlight c %}
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

[1]:https://leetcode.com/problems/evaluate-reverse-polish-notation/
