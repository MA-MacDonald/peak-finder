# peak_finder
simple algorithm to find a peak in single point streaming data

```Python
def make_peak_finder(thresh=0):
    last = 0
    ascent_dist = 0
    ascent_start = 0

    def peak_finder(data, plot):
        data = data[-1]
        nonlocal last, ascent_dist, ascent_start
        if data > last:
            if not ascent_start:
                ascent_start = last
            ascent_dist += 1
        else:
            if ascent_dist:
                peak = last
                ascent_dist = 0
                ascent_start = 0
                if peak - ascent_start > thresh:
                    last = data
                    return peak
                ascent_start = 0
        last = data
        return None

    return peak_finder
    
if __name__ == '__main__':
    my_nums = [3,4,2,13,1,2,5,6,3,8,23,33,100,100,100,99,69,1]
    peaks = [peak_f(data) for data in my_nums]
    print(peaks)
```
