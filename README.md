# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
```
import numpy as np
import math
import scipy.stats

L = list(map(int, input().split()))
N, M = len(L), max(L)

f = [L.count(i) for i in range(M+1)]
sf = sum(f)
p = [f[i] / sf for i in range(M+1)]
mean = np.inner(range(M+1), p)

print("X P(X=x) Obs.Fr Exp.Fr xi")
print("--------------------------")

cal_chi2_sq = 0
for x in range(M+1):
   exp_fr = math.exp(-mean) * mean**x / math.factorial(x)
   E = exp_fr * sf
   xi = ((f[x] - E) ** 2) / E
   cal_chi2_sq += xi
   print(f"{x:2.2f} {exp_fr:2.3f} {f[x]:4.2f} {E:3.2f} {xi:3.2f}")

print("--------------------------")
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print(f"Calculated value of Chi square is {cal_chi2_sq:4.2f}")
print(f"Table value of chi square at 1% level is {table_chi2:4.2f}")
print("The given data can be fitted in Poisson Distribution at 1% LOS" if cal_chi2_sq < table_chi2 else "The given data cannot be fitted in Poisson Distribution at 1% LOS")
```
 

# Output : 

<img width="682" height="620" alt="image" src="https://github.com/user-attachments/assets/90aa30eb-9289-4c44-9c78-a84c0af57e72" />


# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
