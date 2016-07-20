# How to set up your brand new RHEL 7.2 POWER8 system

## Attach your RHEL subscription

```shell
subscription-manager register --username XXXXXXXXXX --password XXXXXXXX
subscription-manager attach --auto
yum update
```

## Install IBM XL Fortran compiler

```shell
mkdir xlfortran
cd xlfortran
tar zxvf IBM_XL_FORTRAN_V15.1.4.0_LINUX_EVAL.tar.gz
./install
```

## Install IBM XL C compiler

```shell
mkdir xlc
cd xlc
tar zxvf IBM_XL_C_CPP_V13.1.4.0_LINUX_EVAL.tar.gz
./install
```

## Install CUDA

```shell
rpm -Uvh cuda-repo-rhel7-7-5-local-7.5-23.ppc64le.rpm
curl https://dl.fedoraproject.org/pub/epel/7/ppc64le/d/dkms-2.2.0.3-34.git.9e0394d.el7.noarch.rpm > dkms-2.2.0.3-34.git.9e0394d.el7.noarch.rpm
curl https://dl.fedoraproject.org/pub/epel/7/ppc64le/l/libvdpau-0.9-1.el7.ppc64le.rpm > libvdpau-0.9-1.el7.ppc64le.rpm
yum install kernel-devel
rpm -Uvh dkms-2.2.0.3-34.git.9e0394d.el7.noarch.rpm libvdpau-0.9-1.el7.ppc64le.rpm
reboot
yum install cuda
```

## Install IBM Engineering and Scientific Subroutine Library (ESSL)

```shell
mkdir essl
cd essl
export IBM_ESSL_LICENSE_ACCEPT=yes
rpm -Uvh essl.3264.rte-5.4.0-0.ppc64le.rpm essl.6464.rte-5.4.0-0.ppc64le.rpm essl.license-5.4.0-0.ppc64le.rpm essl.msg-5.4.0-0.ppc64le.rpm essl.rte.common-5.4.0-0.ppc64le.rpm essl.3264.rtecuda-5.4.0-0.ppc64le.rpm essl.common-5.4.0-0.ppc64le.rpm essl.man-5.4.0-0.ppc64le.rpm essl.rte-5.4.0-0.ppc64le.rpm
```

## Install Puppet agent

```shell
yum install ruby
gem install puppet
which puppet
puppet --version
cp puppet.service /usr/lib/systemd/system/
cp puppet /etc/sysconfig/
puppet resource service puppet ensure=running enable=true
puppet agent --test
```

## Other stuff

```shell
yum install gcc gcc-c++ gcc-gfortran wget yum-utils pciutils
```
