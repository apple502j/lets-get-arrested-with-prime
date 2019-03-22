# How to Decode

- Split into 3 letters (so, 147065 -> [147, 065])
- remove unnecessary 0 (so, 065 -> 65)
- the list of numbers are now bytes
- decode as base64
- decode as Shift-JIS
- Done. You will be arrested by Hyogo prefecture's police.

# Auto-generate
NOTE: Source code below is copylighted, **not Unlicensed**.
Some are taken from http://d.hatena.ne.jp/pashango_p/20090704/1246692091

```python
import random

xrange = range

def is_prime3(q,k=50):
    q = abs(q)
    if q == 2: return True
    if q < 2 or q&1 == 0: return False
    if str(q)[-1] in [0, 2, 4, 5, 6, 8]: return False

    d = (q-1)>>1
    while d&1 == 0:
        d >>= 1
    
    for i in xrange(k):
        a = random.randint(1,q-1)
        t = d
        y = pow(a,t,q)
        while t != q-1 and y != 1 and y != q-1: 
            y = pow(y,2,q)
            t <<= 1
        if y != q-1 and t&1 == 0:
            return False
    return True

from base64 import b64encode as b64

while True:
    SOURCE = '"".join([str(i).zfill(3) for i in b64("while(\'{0}\') alert(\'{1}\');".encode("shift-jis"))])'
    HIRA = "あいうえおかきくけこさしすせそたちつてとなにぬねのはひふへほまみむめもらりるれろやゆよわをん"
    s1 = random.choices(list(HIRA), k=random.randint(3,9))
    s2 = random.choices(list(HIRA), k=random.randint(3,9))
    ns = SOURCE.format(''.join(s1), ''.join(s2))
    res = eval(ns)
    print(s1, s2)
    if is_prime3(int(res)):
        print(ns)
        print(res)
        break
```
