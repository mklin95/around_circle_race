~~~cpp
#include <bits/stdc++.h>
using namespace std;

bool cmp(pair<int, double> a, pair<int, double> b)
{
  return a.second < b.second;
}

int main()
{
  ios::sync_with_stdio(0);
  cin.tie(0); cout.tie(0);

  int p, n; //人數, 圈數
  cin >> p >> n;
  int csize = n; //最多要跑幾趟
  int c[100005] = {0}; //第幾人第幾趟對應跑的圈數
  double a[1005]; //每人單圈秒數
  for(int i = 0; i < p; i++) cin >> a[i];
  double ans = 0; //總秒數
  pair<int, double> s[100005]; //第幾人第幾趟, 對應的單圈秒數

  for(int i = 0; i < n; i++)
  {
    s[i].first = i;
    s[i].second = a[i%p] * pow(1.2, i/p);
  } //先算出每人每趟第一圈的秒數

  for(int i = 0; i < p; i++)
  {
    ans += a[i];
    s[i].second *= 1.1;
    c[i]++;
  } //每人第一趟的第一圈先加上去
  n -= p;

  while(n > 0)
  {
    sort(s, s + csize, cmp); //找出最小秒數

    int tmp = 0; //紀錄這次最佳解的編號
    bool v = 0; //紀錄這個解是否合理
    while(v == 0) //如果不合就繼續找下一個解
    {
      if(s[tmp].first >= p && (c[s[tmp].first-1]) == 0)
        tmp++; //編號+1，找下一個最佳解
      else v = 1;
    }

    ans += s[tmp].second; //總秒數加上去
    c[s[tmp].first]++; //這一趟的圈數+1
    s[tmp].second *= 1.1; //這趟多跑了一圈，秒數乘上去
    n--; //還要處理的圈數-1
  }

  for(int i = 0; i < csize; i++)
    if(c[i]) cout << c[i] << " ";
  cout << ans << endl;

  return 0;
}
~~~
