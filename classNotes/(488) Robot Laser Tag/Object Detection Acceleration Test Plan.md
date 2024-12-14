# YOLO 
- [ ] Try applying a software tool like ONNX or TensorRT to speed up the inference process 
- [ ] Train a smaller model like yolov5-nano on images of cones and the target and measure performance (add some sort of time logging functionality to compare between models)
- [ ] Quantize the YOLOv5 model to INT8 or FP16 precision to reduce computational load.
**Worst Case**
- [ ] Order a USB TPU (https://coral.ai/products/accelerator)

# Kinect 
- [ ] Make sure it is making use of the fastest available usb port on the raspberry pi 
- [ ] Ensure libfreenect is running at the maximum frame rate supported by the Kinect model
- [ ] Minimize processing done during frame capture to avoid delays.
- [ ] Reduce the resolution of RGB/depth frames if high resolution isn’t strictly necessary for your application.