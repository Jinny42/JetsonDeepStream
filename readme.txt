1. DeepStream 4.0.2 for Jetson
* Download .tar

https://developer.nvidia.com/deepstream-download



2. extract

cd Downloads

tar -jxvf deepstream_sdk_v4.0.1_jetson.tbz2 

**********************************************************************

Download github

git clone https://github.com/jinny42/JetsonDeepStream



3. Install Dependency

sudo apt-get update

sudo apt --fix-broken install

sudo apt-get install     libssl1.0.0     libgstreamer1.0-0     gstreamer1.0-tools     gstreamer1.0-plugins-good     gstreamer1.0-plugins-bad     gstreamer1.0-plugins-ugly     gstreamer1.0-libav     libgstrtspserver-1.0-0     libjansson4

sudo apt-get install librdkafka1=0.11.3-1build1

export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

======================================================================

4. Install DeepStream

cd

sudo mv Downloads/deepstream_sdk_v4.0.1_jetson ./

cd deepstream_sdk_v4.0.1_jetson/
sudo tar -xvf binaries.tbz2 -C /
sudo ./install.sh
sudo ldconfig

5. Check !!

cd /opt/nvidia/deepstream/deepstream-4.0/

ls

sudo chmod 777 ./

cp -rf ~/deepstream_sdk_v4.0.1_jetson/sources ./
cp -rf ~/deepstream_sdk_v4.0.1_jetson/samples/ ./
ls

cd /opt/nvidia/deepstream/deepstream-4.0/sources/objectDetector_SSD

* remark) Build & execute

nvidia@nvidia:/opt/nvidia/deepstream/deepstream-4.0/sources/objectDetector_SSD


export CUDA_VER=10.0

make -C nvdsinfer_custom_impl_ssd

* move label text and uff from Downloads folder to current folder.

cp ~/Downloads/JetsonDeepStream/ssdufftest/* ./

* Extract zip file.
unzip sample_ssd_relu6.zip

ls 
--> Check sample_ssd_relu6.uff file.

* Execute 
(Dont' forget power max and sudo jetson_clocks !!!)

deepstream-app -c deepstream_app_config_ssd.txt

-----------------------------------------------------

# usb Camera TEST

## Check you usb camera exits and what device number is.

ls /dev/video*

## After check number, you must check 44 line of the "deepstream_app_config_ssd_usb_f32.txt" file 

deepstream-app -c deepstream_app_config_ssd_usb_f32.txt

-----------------------------------------------------------------------

# Yolo DeapStream plugin Test

cd /opt/nvidia/deepstream/deepstream-4.0/sources/objectDetector_Yolo

./prebuild.sh

export CUDA_VER=10.0

make -C nvdsinfer_custom_impl_Yolo

deepstream-app -c deepstream_app_config_yoloV3_tiny.txt

deepstream-app -c deepstream_app_config_yoloV2_tiny.txt

  
# If you don't mind slow FPS ...

deepstream-app -c deepstream_app_config_yoloV2.txt

deepstream-app -c deepstream_app_config_yoloV3.txt




  




