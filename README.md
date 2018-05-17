# Peak Finder
Lightweight Python algorithm to find peaks in single point streaming data.

```Python
def peak_finder(thresh=0):
    last = 0  # Track last input value
    ascent_dist = 0  # Horizontal distance from last trough.
    ascent_start = None  # Height of last trough.

    def detect_peak(data):
        nonlocal last, ascent_dist, ascent_start
        if data > last:
            if ascent_start is None:
                ascent_start = last
            ascent_dist += 1
        else:
            if ascent_dist:
                peak = last
                ascent_dist = 0
                if (peak - ascent_start) > thresh:
                    last = data
                    ascent_start = None
                    return peak
                ascent_start = None
        last = data
        return None

    return detect_peak
```

## Example:
```Python
import matplotlib.pyplot as plt
import random

pf = peak_finder(10)  # set threshold to 10.
sample_data = random.sample(range(1, 100), 50)
peak_data = [pf(num) for num in sample_data]

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111)

ax.plot(sample_data, marker='^', color='b')
ax.plot(peak_data[1:], marker='o', color='r')

plt.show()
```
<img width="400" src="Media/figure_1.png" alt="hi" class="inline"/> <img width="400" src="Media/figure_2.png" alt="hi" class="inline"/>


