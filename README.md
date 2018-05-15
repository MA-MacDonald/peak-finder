# peak_finder
simple algorithm to find a peak in single point streaming data

```Python
def peak_finder(thresh=0):
    """ Returns initialized function to detect peaks on live streaming data.
       Args:
           thresh (int): The amplitude threshold in which peaks are recognized.
       Returns:
           function object: The function that detects peaks in streaming data.
    """
    
    last = 0  # Track last input value
    ascent_dist = 0  # Distance from last trough.
    ascent_start = None  # Last trough height

    def detect_peak(data):
        """ Returns initialized function to detect peaks on live streaming data.
            Args:
                data (numeric value): Input data point.
            Returns:
                If peak is detected return peak value, else return None
        """
        
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
