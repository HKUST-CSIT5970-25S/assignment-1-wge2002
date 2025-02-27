[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Wang Ge
### Student Id: 21091208
### Email: gwangbd@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

My answer: To test the CPU performance, we choose the Phoronix Test Suite. We use the compression rate of the 7zip. To test the Memory performance, we also choose the Phoronix Test Suite. We choose to test the action of adding the integer.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance(MIPS) | Memory performance(MB/s)|
    | ----------- | --------------------  | ----------------------- |
    | `t2.micro`  |         3537          |        10533.81         |
    | `t2.medium` |         9756          |        18751.41         |
    | `c5d.large` |         7537          |        13809.56         |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |      2860      |   0.283  |
    | `m5.large` - `m5.large`   |      4960      |   0.155  |
    | `c5n.large` - `c5n.large` |      4960      |   0.151  |
    | `t3.medium` - `c5n.large` |      2130      |   0.653  | (c5n.large as the server)If we change t3.medium as server,the result is 2200, 0.668. We think no matter which instance as server the result is the same.
    | `m5.large` - `c5n.large`  |      3190      |   0.530  | (c5n.large as the server)
    | `m5.large` - `t3.medium`  |      3920      |   0.191  | (t3.medium as the server)

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |     32.2       |  58.937  |
    | N. Virginia - N. Virginia |     4260       |  0.242   |
    | Oregon - Oregon           |     4570       |  0.187   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
