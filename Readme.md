# Touchscreen Calibration on Miosix (mxgui)

Implementation of an interactive **touchscreen calibration mechanism** for the mxgui graphical framework running on the **Miosix RTOS**.

The project extends the original touchscreen driver to support **runtime calibration**, allowing the system to adapt to different touchscreen panels by computing calibration parameters dynamically.

---

## Overview

In the original driver, touchscreen coordinates were converted using fixed constants (`xmin`, `xmax`, `ymin`, `ymax`).  
This project introduces a calibration procedure that computes these parameters automatically by collecting raw touchscreen data during an interactive calibration process. 

The calibration program displays reference points on the screen and records the **raw coordinates** returned by the touchscreen controller. These values are then used to compute the parameters needed to correctly map raw ADC readings to display coordinates. 

---

## Modified Files

The following files were modified to implement the calibration mechanism:

- `main.cpp`  
  Implements the interactive calibration program and computes the calibration parameters.

- `mxgui/drivers/event_st25dvdiscovery.h`  
  Extended the touchscreen event structure to include **raw coordinates**.

- `mxgui/level2/input.h`  
  Added the method to configure calibration parameters:
  ```cpp
  setTouchscreenCalibration(xMin, xMax, yMin, yMax);
