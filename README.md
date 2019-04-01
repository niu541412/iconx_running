# iconx_running
三星iconx跑步数据的速度信息计算
```c
(tt, vv) = readcol("running.dat", 1, 2);
tt1 = tt - tt[0];
tt2 = tt1 / 1000. / 60.;
ss1 = [0: length(vv): 1.0];
for (i = 1; i < length(vv); i++) {
  ss1[i] = ss1[i - 1] + (tt2[i] - tt2[i - 1]) * (vv[i - 1] + vv[i]) / 2. * 60 / 1000.;
}
m = 0;
n = 1;
for (i = 0; i < length(vv); i++) {
  if (ss1[i] >= n) {
    k = (tt2[i] - tt2[m]) / ((ss1[i] - ss1[m]));
    m = int(floor(k));
    s = (k - floor(k)) * 60;
    () = printf("%2dkm:", n);
    for (j = 0; j < round((k - 3) * 10); j++)
      () = printf("▓");
    () = printf("%d\'%.f\" \n", m, s);
    m = i;
    n = n + 1;
  }
  if (i == length(vv) - 1)
    () = printf("toal distance: %.1fkm\n", ss1[-1]);
};
```
