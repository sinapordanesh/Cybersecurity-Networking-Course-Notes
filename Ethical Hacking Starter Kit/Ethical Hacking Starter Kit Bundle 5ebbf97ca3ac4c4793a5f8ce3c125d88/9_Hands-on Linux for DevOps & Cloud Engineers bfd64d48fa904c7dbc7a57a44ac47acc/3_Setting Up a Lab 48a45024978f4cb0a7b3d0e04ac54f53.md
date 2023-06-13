# 3_Setting Up a Lab

- AWS Account

## Overview of virtual/private cloud (VPC)

![Screenshot 2023-06-02 at 5.02.33 PM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-02_at_5.02.33_PM.png)

## Subnets

![Screenshot 2023-06-02 at 5.15.08 PM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-02_at_5.15.08_PM.png)

![Screenshot 2023-06-02 at 5.15.21 PM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-02_at_5.15.21_PM.png)

![Screenshot 2023-06-03 at 9.52.35 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_9.52.35_AM.png)

![Screenshot 2023-06-03 at 9.52.01 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_9.52.01_AM.png)

![Screenshot 2023-06-03 at 9.52.50 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_9.52.50_AM.png)

## Security Groups and Internet Gateway

![Screenshot 2023-06-03 at 9.54.12 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_9.54.12_AM.png)

![Screenshot 2023-06-03 at 9.54.23 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_9.54.23_AM.png)

![Screenshot 2023-06-03 at 9.54.36 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_9.54.36_AM.png)

![Screenshot 2023-06-03 at 10.04.54 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.04.54_AM.png)

![Screenshot 2023-06-03 at 10.05.04 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.05.04_AM.png)

![Screenshot 2023-06-03 at 10.08.02 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.08.02_AM.png)

![Screenshot 2023-06-03 at 10.08.12 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.08.12_AM.png)

## Overview of EC2

![Screenshot 2023-06-03 at 10.09.40 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.09.40_AM.png)

![Screenshot 2023-06-03 at 10.09.55 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.09.55_AM.png)

![Screenshot 2023-06-03 at 10.14.52 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.14.52_AM.png)

![Screenshot 2023-06-03 at 10.15.09 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.15.09_AM.png)

![Screenshot 2023-06-03 at 10.31.46 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.31.46_AM.png)

## Create your lab

![Screenshot 2023-06-03 at 10.34.53 AM.png](3_Setting%20Up%20a%20Lab%2048a45024978f4cb0a7b3d0e04ac54f53/Screenshot_2023-06-03_at_10.34.53_AM.png)

- clone the “https://github.com/codered-by-ec-council/Hands-on-Linux-for-DevOps-Cloud-Engineers.git”
- Navigat to the `/codred/Hands-on-Linux-for-DevOps-Cloud-Engineers/lab-terraform` folder and run the following command to initialize terraform `terraform init`
- `terraform plan`
- `terraform apply`
- `<output ip address from previous command>`