<strong>1. Compute the maximum likelihood probability of the phrase du hast mich gefragt‘you asked me’according to a second-order Markov model.</strong>

P(du) = 19/64
P(hast) = 14/64
P(mich) = 9/64
P(gefragt) = 3/64

P(du hast mich gefragt) = 0.296875 * 0.21875 * 0.140625 * 0.046875 = 0.00042808055

<strong>2. Use negative logarithms to compute 1/2561/8181, showing your work.</strong>

Adding their logs and then exponentiating:
From the example:

``In [43]: math.log(.5) + math.log(.01)<p>

Out[43]: -5.298317366548036<p>

In [44]: math.exp(-5.298317366548036)<p>

Out[44]: 0.005000000000000002``<p>

and then with 1/256 * 1/8181:


``In [45]: math.log(0.00390625) + math.log(0.00012223444)<p>
Out[45]: -14.554747162353262<p>
In [46]: math.exp(-14.554747162353262)<p>
Out[46]: 4.774782812499997e-07``

