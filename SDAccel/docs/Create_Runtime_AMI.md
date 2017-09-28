# Create a Runtime AMI Starting with an Amazon Linux AMI                          

## 1. Launch a Runtime Instance & Install Required Packages 

* Launch an F1 instance using an [Amazon Linux AMI](https://aws.amazon.com/marketplace/pp/B00635Y2IW)
* Install the required updates and pacckages

````
  $ sudo yum update
  $ sudo yum install git
  $ sudo yum install gcc
  $ sudo yum install gcc-c++          
  $ sudo yum install kernel-headers   
  $ sudo yum install kernel-devel     
  $ sudo yum --enablerepo=epel install ocl-icd ocl-icd-devel opencl-headers
  $ sudo mkdir -p /etc/OpenCL/vendors/
````  
                                                              
## 2. Copy required Xilinx SDAccel Runtime Libraries to the Instance and Reboot your Runtime Instance. 
<!--- # ENHANCEMENT: We should consider whether these files can be added to github --->

* On an instance running [FPGA Developer AMI](https://aws.amazon.com/marketplace/pp/B06VVYBLZZ) or on a local machine with access to a Xilinx SDAccel Tools Installation copy required files into a single directory:

````
   $ mkdir -p xlnxrte/lib/lnx64.o
   $ mkdir -p xlnxrte/runtime/bin
   $ cp $XIILNX_SDX/lib/lnx64.o/libstdc++.so* xlnxrte/lib/lnx64.o/.
   $ cp $XIILNX_SDX/lib/lnx64.o/libxilinxopencl.so xlnxrte/lib/lnx64.o/.
   $ cp $XIILNX_SDX/runtime/bin/xclbinsplit xlnxrte/runtime/bin         
   $ cp $XIILNX_SDX/runtime/bin/xclbincat xlnxrte/runtime/bin
````

* Copy xlnxrte directory created to /home/ec2-user/ on your Runtime Instance.
* Reboot your Runtime Instance to ensure all upgrades are running.

## 3. Install Runtime Drivers and run your FPGA accelerated application on your Runtime Instance. 
* Log back on to the Runtime Instance:

```
  $ export XILINX_SDX=/home/ec2-user/xlnxrte
````
* You should be able to [run your FPGA accelerated application as described here](https://github.com/aws/aws-fpga/tree/master/SDAccel#runonf1), without needing to launch a new F1 instance


## 4. Create your Runtime AMI based on your Instance.

* Once you have all your application details you should be able to create a Runtime AMI from your Runtime Instance as specificed [here](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html):



