# Main Portion of Code 
```python
from machine import ADC, Pin
import time
import numpy as np






# Detect a red laser hit based on intensity changes

def detect_red_laser_hit(light_sensor_data):
    # Calibrate baseline light level with room lighting
    baseline = calibrate_baseline(light_sensor_data)
    red_spike_threshold = baseline + 0.4  # 0.4V above the calibrated baseline; can adjust
    rate_of_change_threshold = 0.3  # Detects rapid increases typical of lasers (in volts)
    # shadow_threshold = 0.01  # Minimum rate of change to detect shadows
    detection_duration = 1  # Minimum duration (in seconds) for confirmed hit
    stop_duration = 5  # Stop for 5 seconds upon confirmed hit
    hit_detected = False
    start_time = None
    window_size = 5  # Window size for moving average
    recent_readings = []

    while True:
        # Get the current light intensity reading
        light_intensity = light_sensor_data.get()

        # Get camera readings
        # opposing_robot_visible, laser_detected = camera_data.detect_robot_and_laser()  # Camera logic

        # Apply a moving average for noise reduction
        recent_readings.append(light_intensity)
        if len(recent_readings) > window_size:
            smoothed_light = moving_average(recent_readings, window_size)[-1]
            rate_of_change = smoothed_light - recent_readings[-2]  # Change in intensity

            # Detect a shadow by looking for gradual changes
            # if abs(rate_of_change) < shadow_threshold:
                # print("Passing through a shadow...")
                # hit_detected = False
                # continue

            # Detect a red laser hit based on intensity spike and rate of change
            if smoothed_light > red_spike_threshold and rate_of_change >= rate_of_change_threshold:
                if not hit_detected:
                    start_time = time.time()
                    hit_detected = True
                elif time.time() - start_time >= detection_duration:
                    print("Red laser hit detected!")
                    stop_movement()
                    time.sleep(stop_duration)
                    resume_movement()
                    hit_detected = False
                    start_time = None
            else:
                # Reset detection if no sustained hit is detected
                hit_detected = False
                start_time = None

# Calibrate baseline light level over a period
def calibrate_baseline(light_sensor_data, calibration_time=2):
    readings = []
    start_time = time.time()
    while time.time() - start_time < calibration_time:
        readings.append(light_sensor_data.get())
        time.sleep(0.1)  # Sample every 100ms
    baseline = sum(readings) / len(readings)
    print(f"Calibrated baseline light level: {baseline}")
    return baseline


# Moving average function to smooth out the readings
def moving_average(readings, window_size):
    return np.convolve(readings, np.ones(window_size) / window_size, mode='valid')



```

# Minimizing False Positives
the algorithm minimizes false positives by checking for the following criterea
- **Enemy Detection:** since the solar panel is mounted on the front of the robot as well as the camera, it will always be the case that the opposing robot will always be in camera view if it is in a firing position. Therefore we check to see if we have detected an enemy robot in our FOV 
- **Continuous Calibration to Ambient Light**: This is used to smooth out the baseline voltage of our solar panel as the ambient light levels fluctuate
- **Moving Average:** this is used to smooth out the spikes that come from laser hits to ensure that a voltage spike is from a significant and **sustained** 
- **Voltage Spike threshold**: we will conduct testing to select a threshold value that isn't too sensitive but can also pick up on laser hits accurately 

### Possible additions
- given that we can get a pretty reasonable idea of how far the enemy robot is, we can use the inverse square law to adjust the voltage spike threshold value to what would be expected for a laser fired from that distance
