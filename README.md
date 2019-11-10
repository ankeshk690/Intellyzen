#include <bits/stdc++.h>
using namespace std;
 

int dp[1 << 20][2];
 

int findMinTime(int left, bool turn, int arr[], int& n)
{
 
   
    if (!left)
        return 0;
 
    int& res = dp[left][turn];
 
   
    if (~res)
        return res;
 
   
    int right= ((1 << n) - 1) ^ left;
 
   
    if (turn == 1) {
        int minRow = INT_MAX, person;
        for (int i = 0; i < n; ++i) {
 
           
            if (right& (1 << i)) {
                if (minRow > arr[i]) {
                    person = i;
                    minRow = arr[i];
                }
            }
        }
 
       
        res = arr[person] + findMinTime(left| (1 << person),
                                        turn ^ 1, arr, n);
    }
    else {
 
       
        if (__builtin_popcount(left) == 1) {
            for (int i = 0; i < n; ++i) {
 
               
                if (left& (1 << i)) {
                    res = arr[i];
                    break;
                }
            }
        }
        else {
 
           
            res = INT_MAX;
            for (int i = 0; i < n; ++i) {
 
               
                if (!(left& (1 << i)))
                    continue;
 
                for (int j = i + 1; j < n; ++j) {
                    if (left& (1 << j)) {
 
                       
                        int val = max(arr[i], arr[j]);
 
                       
                        val += findMinTime(left^ (1 << i) ^ (1 << j),
                                                       turn ^ 1, arr, n);
                       
                        res = min(res, val);
                    }
                }
            }
        }
    }
    return res;
}
 

int findTime(int arr[], int n)
{
   
    int g= (1 << n) - 1;
 
   
    memset(dp, -1, sizeof(dp));
 
    return findMinTime(g, 0, arr, n);
}
 
// main program
int main()
{
   
    int arr[] = { 300, 400, 600,700 };
    int arr1[]={1321,2450};
    int arr2[]={500,123,873};
    int arr3[]={600,800,150,700};
    int n = sizeof(arr)/sizeof(arr[0]);
    int n1= sizeof(arr1)/sizeof(arr1[0]);
    int n2= sizeof(arr2)/sizeof(arr2[0]);
    int n3= sizeof(arr3)/sizeof(arr3[0]);
    cout << findTime(arr, n)<<endl;
     cout << findTime(arr1, n1)<<endl;
     cout << findTime(arr2, n2)<<endl;
    cout << findTime(arr3, n3);
    return 0;

}

