# Create a Runtime AMI Starting with an Amazon Linux AMI                          

## 
Start launching an instance with an [Amazon Linux AMI](https://aws.amazon.com/marketplace/pp/B00635Y2IW)


````
  $ sudo yum update
  $ sudo yum install git
  $ sudo yum install gcc
  $ sudo mkdir -p /etc/OpenCL/vendors/
  $ sudo yum install gcc-c++          
  $ sudo yum install kernel-headers   
  $ sudo yum install kernel-devel     
  $ sudo yum --enablerepo=epel install ocl-icd ocl-icd-devel opencl-headers
  $ aws configure                                                          
````                                                                       

Reboot instance to ensure all upgrades to instance work as expected


<-- We should consider whether these files can be added to github -->

On an instance or local machine  with access to a XILINX 2017.1_sdx SDAccel Tools Installation or using an FPGA Dev AMI:

   mkdir -p xlnxrte/lib/lnx64.o
   mkdir -p xlnxrte/runtime/bin
   cp $XIILNX_SDX/lib/lnx64.o/libstdc++.so* xlnxrte/lib/lnx64.o/.
   cp $XIILNX_SDX/lib/lnx64.o/libxilinxopencl.so xlnxrte/lib/lnx64.o/.
   cp $XIILNX_SDX/runtime/bin/xclbinsplit xlnxrte/runtime/bin         
   cp $XIILNX_SDX/runtime/bin/xclbincat xlnxrte/runtime/bin


Copy xlnxrte directory to your Runtime instance.

Reboot instance to ensure all upgrades to instance work as expected


Log back on to the runtime instance:

  $ export XILINX_SDX=/home/ec2-user/xlnxrte
  $ git clone https://github.com/aws/aws-fpga.git
  $ cd aws-fpga/
  $ source sdaccel_setup.sh

You should be able to execute your application as specified in:

https://github.com/aws/aws-fpga/tree/master/SDAccel#runonf1


Once you have all your application details you should be able to create an AMI from your instnace as specificed here:

http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html


User of AMI would need:

  $ cd aws-fpga/
  $ source sdaccel_setup.sh

And execute application.

