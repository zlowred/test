test
====
scrollPos = 0; scrollPos <= 24; scrollPos++
dg = 0; dg < 3; dg++
dp = scrollPos / 4 + dg
d = (x / (int)Math.pow(10, dp)) % 10
shift = (scrollPos % 4) - dg * 4
line |= charset[d * 5 + ln] >> shift
or
line |= charset[d * 5 + ln] << -shift
