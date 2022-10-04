## [Triple XOR](https://www.codechef.com/submit/ABCXOR)

This problem is part of coimbatorics

### Problem
You are given two integers N and K. Find number of ordered triplets (A, B, C) that satisfy the following conditions:

* $0 \le A$,B, $C \lt 2^N$  
* A, B,C are distinct.
* A⊕B⊕C=K
Here, ⊕ denotes the bitwise XOR operation.

### Input Format
The first line contains a single integer T — the number of test cases. Then the test cases follow.
The first and only line of each test case contains two space-separated integers N and K — the parameters mentioned in the statement.

### Output Format
For each test case, output on a new line the number of triplets that satisfy the given conditions.


#### Solution

I went thinking like this. If a bit in K is 0, then I have 4 options for the same bit in A,B,C → 000, 011, 101, 110. If a bit in K is 1, then I also have 4 options 111, 100, 010, 001.
All triplets that xor to K is then 4^{n}. Of course, the task says numbers in a triplet need to be distinct. So I subtract all cases when 2 numbers are the same, which is 
3*(2^{n}-1) ->  there are 2^n possible numbers, and if two are the same and third one is K (without a loss of generality A=B=x and C=K) I have 2^n-1 choices for x (multiplied by 
3 because there are 3 options for which number is K). I also want to exclude (K,K,K) from the final count so I will subtract 1. 

4^n-3*[(2^n-1)]-1

```Java
import java.util.*;
import java.lang.*;
import java.io.*;

class Codechef
{
	public static void main (String[] args) throws java.lang.Exception
	{
		int T;
		Scanner in = new Scanner(System.in);
		T=in.nextInt();
// 		in.nextLine();
		while(T-->0)
		{
		    int n=in.nextInt();
		    int k=in.nextInt();
		    long ans=binaryPow(4,n);
		    long ans2=binaryPow(2,n);
		    System.out.println(ans-3*(ans2-1)-1);
		}
	}
	static long binaryPow(long a,long b){
	    if(b==0)return 1;
	    long res=binaryPow(a,b/2);
	    if(b%2==0){
	        return res*res;
	    }
	    else return res*res*a;
	}
}
```



