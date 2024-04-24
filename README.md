# VaishnaviSabat_Girl-Hackathon_2024

**Problem Statement :**
A Simulator model which shows a System on a Chip (SoC) consisting of a CPU and a IO peripheral accessing System memory through an weighted arbiter. The SoC components are connected through a Network on Chip (NOC). The NOC has a bi-direction port per component and routes traffic between to and fro from System memory. Each interface has buffering to account for latency of data transfer to and from System memory. Data traffic flows are between CPU to System Memory,IO peripherals to System memory. The weighted round robin arbiter feeds traffic from both CPU and IO to system memory. The traffic pattern in the NOC depends on the types of workloads running on CPU and IO. Given the vast possibilities of different traffic patterns, designing a NOC that is area and power efficient and yet able to achieve desired performance in terms of latency (time to retrieve data from memory) and bandwidth (throughput or the quantity of data transferred per second) is challenging. An over designed NOC with bigger buffers where not all entries are occupied is area inefficient and predetermined arbitration weights will impact both bandwidth and latency. Our goal here is to come up with the NOC design that is best suited for target workloads running on this system.  
![Screenshot (572)](https://github.com/Vaisno1602/VaishnaviSabat_Girl-Hackathon_2024/assets/113321729/2eb7f7b8-a66d-476f-8118-7d33239d6ebf)



**To set up the environment ans execute the code following steps should be followed :**
1. Installation of Python environmet setup
2. Installation of required packages (pandas and numpy)
3. Prepare Interface Monitor Output (The interface monitor output data should be arranged as per the specified format in the code comments. A text file can also be created with the data or generated programmatically.
4. Run the Code (Copy the code snippet into a Python script file (e.g., measure_latency_bandwidth.py) and execute it using Python: python measure_latency_bandwidth.py)
5. Interpret Results
6. Debugging and Optimization (For improved efficiency ad accuracy the code should be debugged and optimized if needed)
7. Integration with Larger System
   

**Approach for algorithm :**
A linear search of the interface monitor output is the method utilized in the pseudocode to determine average delay and bandwidth. It parses the data and transaction type for each line of the output iteratively, then looks for the matching data transaction in the output. After it locates the delay, it computes it and modifies the overall latency and the amount of bytes transferred in accordance. Using the entire values accumulated, it finally computes the average delay and bandwidth.


**Reinforced Learning Framework to arrive at optimal parameters :**
1. **States / Behaviours-**
    Buffer Occupancy: Percentage of buffer occupancy for each buffer.
    Arbitration Rates: Current arbitration rates at the input of the arbiter for CPU and IO.
    System Power Limit: Binary value indicating if the system power exceeds the threshold.
    Throttling Frequency: Frequency of throttling occurrences.
2. **Actions-**
    Adjust Buffer Sizes: Modify buffer sizes to optimize occupancy.
    Set Arbiter Weights: Adjust weights dynamically to balance traffic.
    Throttle Frequency: Control the frequency of throttling based on power threshold.
    Adjust Operating Frequency: Dynamically adjust the operating frequency of the NOC.
3. **Rewards-**
    Latency Optimization: Negative reward for increased latency beyond the desired minimum.
    Bandwidth Utilization: Positive reward for achieving or exceeding 95% of the maximum bandwidth.
    Buffer Efficiency: Positive reward for maintaining buffer occupancy close to 90%.
    Throttling Penalty: Negative reward for excessive throttling occurrences.
    Power Consumption: Negative reward for exceeding power limits.
4. **RL Algorithm Selection-**
    A Deep Deterministic Policy Gradient (DDPG) algorithm version, like Twin Delayed DDPG (TD3), might be a good fit for this problem given the continuous state and action spaces, as well as the requirement for effective exploration and exploitation. DDPG-based algorithms have demonstrated effectiveness in comparable optimization challenges and are capable of effectively managing high-dimensional state and action spaces. Effective decision-making in this complex context is made possible by their ability to learn a deterministic policy and value function approximation. Furthermore, during training, stability and convergence can be enhanced by TD3's improvements including target policy smoothing and delayed updates.
![RL_Framework](https://github.com/Vaisno1602/VaishnaviSabat_Girl-Hackathon_2024/assets/113321729/66b58496-4797-47c0-964c-c063718c4ce4)



**Proof of Correctness  :**
Let ti represent timestamp of transaction i,  typei represent the transaction type of transaction i, where typei is “Rd” for read transactions and “Wr” is for write transactions, datai represent the data associated with transaction i and  Li represent latency of transaction i, defined as the difference between the timestamp of the read transaction and the corresponding data transaction
total_latency=0, total_bytes=0, total_transactions=0
For each line i in interface_monitor_output : Parse line i to extract ti, typei, datai      
                                              If typei is “Rd” : Find corresponding data transaction j in the interface monitor output
                                              Calculate latency Li=tj - ti, Increment total_latency by Li  
                                              If typei is “Wr” : Increment total_bytes_transactions by 1
average_latency = total_latency/total_transactions
average_bandwidth = total_bytes_transferred/total_transactions


**Complexity Analysis :**
**Time Complexity-**
        The initialization and calculation of metrics steps take O( 1 ) time
        The processing of the interface monitor output takes O( n ) time, where n is the number of lines in the ‘interface_monitor_output’
        Therefore the overall complexity of given code is O( n ), where n is the number of lines in the ‘interface_monitor_output’
**Space Complexity-** 
        total_latency, total_bytes_transferred, total_transactions are scalar variables and occupy constant space. Therefore, their combined space complexity is 𝑂(1)
        interface_monitor_output represents the input data structure containing the monitor output. Its space complexity depends on the size of the input data and the number of lines it contains which is O( m ) where m is length of input data.
        Overall, the space complexity of the given code is the sum of the space required for variables and data structures:    O( 1 ) + O( m )= O( m )
        So, the space complexity of the code is O( m ) where m is the size of interface_monitor_output


        
**---------------------------------------------------------------------------------------------END----------------------------------------------------------------------------------------------------------------**







   
