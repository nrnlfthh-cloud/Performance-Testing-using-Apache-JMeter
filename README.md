# Performance-Testing-using-Apache-JMeter
For testing web applications, JMeter is one of the popular open-source performance testing tools. One of its benefits is that it can simulate a high load with many virtual users. Multiple test types (Load, Stress, Spike, Soak) are supported and there is also non-GUI mode for effective high-load performance.

# 1.0	Introduction

In today's world, a modern web application's performance, scalability, and stability are the factors that determine its success. No matter how good the service is, it will always lead to poor user experience, lost sales, and damaged reputation if the response time is slow or the system fails. Hence, this technical assignment aims to perform an in-depth, evidence-based performance analysis of a web application by designing and executing a rigorous test plan to identify the critical performance indicators (KPIs), uncover the bottlenecks, and classify the failure modes under stress.
The primary tool used in the study was the industry-standard software Apache JMeter, which allowed for three different performance testing approaches: first, a Load Test to set up the performance baseline under expected peak traffic. Next, a Stress Test to find out the highest limit of the system and its point of saturation by overloading it and the last one is Spike Test to examine the application's instant resistance to sudden, overwhelming user activity influxes.
For testing web applications, JMeter is one of the popular open-source performance testing tools. One of its benefits is that it can simulate a high load with many virtual users. Multiple test types (Load, Stress, Spike, Soak) are supported and there is also non-GUI mode for effective high-load performance. Listeners and dashboard reports are well integrated. JMeter was chosen for this assignment for its features and accessibility.
 
# 2.0 Hardware/Software Configuration

•	Operating System: Windows 11
•	Tool Version: Apache JMeter 5.6.3
•	Execution Mode: GUI for Load Test, non‑GUI for Stress & Spike Tests
•	Java Version: OpenJDK 17
•	Target Application: dummyjson[.]com

# 3.0 Test Elements Used in JMeter	

•	Thread Group
•	HTTP Request Samplers
•	Duration Assertion
•	Constant/Spike Load Profiles
•	Listeners (Dashboard Report)

# 4.0 Test Types & Methodology

# 4.1 Load Test
•	Purpose: To identify system behaviour under expected normal load.

Configuration:
•	Number of Users: 100
•	Ramp-Up: 60
•	Duration: 300
•	Summary: The load test was designed to evaluate how the application performs under normal, expected user traffic. During execution, the system maintained stable response times, with average response time staying within acceptable limits. Throughput increased gradually as virtual users ramped up, indicating the server could scale under predictable load. No significant errors were observed, and the success rate was approximately 100%, showing that the application could handle continuous traffic without noticeable degradation. Response time graphs showed minor fluctuations, but no severe latency spikes. The application performs reliably under normal load, with consistent throughput, low error rates, and stable response times.

# 4.2 Stress Test
•	Purpose: To identify the breaking point of the system by continuously increasing load beyond normal usage. After adding a Duration Assertion (1000 ms), the test was able to differentiate between acceptable and degraded performance.

Configuration:
•	Number of Users: 700
•	Ramp-Up: 30
•	Duration: 1000
•	Summary: As the number of concurrent users increased, the system initially handled the load well. However, once the threshold was exceeded:

	Response times rise significantly.
	Latency spiked beyond 1000 ms.
	Failures began to appear due to timeout and assertion violations.
	Throughput dropped as the server struggled to keep up.

This indicates that the system has a clear performance ceiling. Beyond a certain concurrency level, the API could no longer maintain stable responses and began returning errors. 

# 4.3 Spike Test
•	Purpose: To evaluate how the application behaves when it experiences a sudden and extreme increase in user load within a very short period. Unlike gradual load or stress tests, a spike test focuses on the system’s immediate reaction to abrupt traffic surges, such as those caused by viral user activity, unexpected promotions, or sudden spikes in real-world demand.

Configuration:
•	Number of Users: 8000
•	Ramp-Up: 1
•	Duration: 60
•	Summary: The spike test evaluated how the DummyJSON API responds when user load increases suddenly from normal traffic to a very high level within one second. The test was executed using a single Thread Group with 8000 virtual users, a 1-second ramp-up, and a 60-second duration. A single GET request to /products was used, with tightened timeout settings to reveal performance weaknesses under extreme load.
Overall, the spike test demonstrated that DummyJSON performs adequately under moderate load but becomes unstable when exposed to abrupt high traffic surges. The results reveal expected bottlenecks such as delayed response processing, increased latency, and elevated error rates. These findings confirm that the system is not optimized for handling sudden traffic spikes, which is typical for public mock APIs.

# 5.0 Performance Test Comparison

This section provides a comparative overview of the three performance tests conducted which is Load Test, Stress Test, and Spike Test to evaluate how the system behaves under different traffic conditions. The purpose of this comparison is to highlight the differences in user load, traffic patterns, and system response characteristics for each test type. By analysing these tests side by side, we can clearly observe how the system performs under normal operational load, progressively increasing heavy load, and sudden extreme load. This comparison helps identify performance thresholds, potential bottlenecks, and the system’s overall resilience, providing a clearer understanding of its stability and scalability across various real-world scenarios.

# 6.0 Results and Evidence
# 6.1 Load Test Result (GUI mode)
<img width="940" height="376" alt="image" src="https://github.com/user-attachments/assets/16c17ce8-e2e1-4c4b-9e27-8692cc07831e" />
Thread Group Configuration (Load Test): Screenshot displaying the settings for the Load Test's Thread Group in JMeter, configured for 100 users, a 60-second ramp-up period, and a 300-second duration.

<img width="940" height="122" alt="image" src="https://github.com/user-attachments/assets/9906416c-8262-4751-9091-897f3af27a2b" />
Constant Timer Configuration (Load Test): Screenshot of the Constant Timer used in the Load Test, which introduces a 1000 millisecond delay between requests.

<img width="940" height="319" alt="image" src="https://github.com/user-attachments/assets/31240b92-f505-47d9-be2d-88410273bca5" />
Response Assertion Configuration (Load Test): Screenshot showing the Response Assertion, configured to check for a successful HTTP Response Code (200).

<img width="940" height="288" alt="image" src="https://github.com/user-attachments/assets/a6201969-68da-456c-987d-3b24b140534a" />
HTTP Request Sampler (GET /products): Screenshot detailing the first HTTP Request Sampler, configured for a GET request to the path /products.

<img width="940" height="291" alt="image" src="https://github.com/user-attachments/assets/773172ab-575f-4eec-a6e5-897517dd4682" />
HTTP Request Sampler (GET /products/1): Screenshot detailing the second HTTP Request Sampler, configured for a GET request to the path /products/1.

<img width="940" height="225" alt="image" src="https://github.com/user-attachments/assets/daaa6ab3-fbb6-4731-8760-d68b52de7e6c" />
Aggregate Report (Load Test): Screenshot of the Aggregate Report results for the Load Test, showing an overall error rate of 0.00% and an average response time of 57 ms for 200 samples.

<img width="940" height="430" alt="image" src="https://github.com/user-attachments/assets/7204e643-30cd-40be-a5ca-c94ef09b0c29" />
Response Time Graph (Load Test): Screenshot of the Response Time Graph, illustrating minor fluctuations but stable response times for both /products and /products/1 requests under normal load.

# 6.2 Stress Test Result (Non-GUI mode)

<img width="940" height="372" alt="image" src="https://github.com/user-attachments/assets/f286776f-2e25-4890-bc47-4caf779c72d9" />
Thread Group Configuration (Stress Test): Screenshot displaying the settings for the Stress Test's Thread Group, configured for 700 users, a 30-second ramp-up, and a 200-second duration.

<img width="940" height="469" alt="image" src="https://github.com/user-attachments/assets/d2b9fc6b-2544-4e0d-a8f8-9bdc72fdc7fb" />
<img width="940" height="118" alt="image" src="https://github.com/user-attachments/assets/3846f62b-34c4-4fcd-bd74-5384be912128" />
JMeter HTML Report Generation Console (Stress Test): Console output of the command used to generate the HTML dashboard report from the Stress Test result file (result_stress.jtl).

<img width="940" height="397" alt="image" src="https://github.com/user-attachments/assets/0c9d7b90-5d99-45c0-a0ae-478eb73bb686" />
JMeter Dashboard - APDEX and Summary (Stress Test - Initial Run): Screenshot of the initial Stress Test dashboard report, showing an APDEX of 0.966 and a 100% pass rate before the Duration Assertion correction.

<img width="940" height="447" alt="image" src="https://github.com/user-attachments/assets/8e78a6c5-c9cc-4d0e-bb8b-05be6dbc603d" />
I did some correction on my Apache Jmeter setting where I add the duration assertion and set the duration in millisecond to 1000.
So, here’s the result:
<img width="940" height="409" alt="image" src="https://github.com/user-attachments/assets/099ca99e-2e23-4a22-8822-4e64a9e68323" />
<img width="940" height="393" alt="image" src="https://github.com/user-attachments/assets/6f16df33-7177-4dce-bb13-35092101b074" />
JMeter Non-GUI Execution Console (Stress Test - Corrected Run): Console output from the corrected non-GUI execution of the Stress Test after adding a Duration Assertion of 1000 ms, showing a total failure percentage of 4.94%.

<img width="940" height="195" alt="image" src="https://github.com/user-attachments/assets/9ab516e4-76f1-4d03-9c86-4c682c1003df" />
<img width="940" height="432" alt="image" src="https://github.com/user-attachments/assets/c5c42cc0-efa0-48fb-997a-c63fba4408fb" />

# 6.3 Spike Test Result (Non-GUI mode)

<img width="940" height="371" alt="image" src="https://github.com/user-attachments/assets/c2ec0c0b-2c0c-4283-abba-f3897076ace9" />
Thread Group Configuration (Spike Test): Screenshot displaying the settings for the Spike Test's Thread Group, configured for 8000 users, a 1-second ramp-up, and a 60-second duration.

<img width="940" height="259" alt="image" src="https://github.com/user-attachments/assets/114c9815-6887-4501-88ae-8d0ef27b8725" />
HTTP Request Sampler (Spike Test): Screenshot detailing the HTTP Request Sampler used in the Spike Test, configured for a GET request to the path /products.

<img width="940" height="248" alt="image" src="https://github.com/user-attachments/assets/7e8750f9-d466-43e3-9ea1-1ab3acd11746" />
<img width="940" height="432" alt="image" src="https://github.com/user-attachments/assets/911f26a1-c65f-4b6a-abf1-77627971ed4d" />
JMeter Non-GUI Execution Console (Spike Test): Console output from the non-GUI execution of the Spike Test, showing a 100.00% error rate in the final summary.

<img width="940" height="488" alt="image" src="https://github.com/user-attachments/assets/194fc84f-0c9f-4538-9694-4f61e46f7db1" />

# 7.0 Summary
The comprehensive performance analysis of the DummyJSON API, utilizing Load, Stress, and Spike tests with Apache JMeter, reveals clear performance characteristics under various traffic conditions.

Load Test: The system performed reliably under a normal expected load of 100 users over 300 seconds. The results demonstrated stable response times (average 57 ms), a 100% success rate (0.00% error), and consistent throughput, confirming the API's stability under normal operating conditions

Stress Test: Pushing the system beyond normal capacity with 700 users over 1000 seconds exposed its limits. The corrected run, with a 1000 ms Duration Assertion, resulted in a 4.94% failure rate, with errors arising because operations lasted too long. This indicates that the system begins to degrade under prolonged heavy load, with response times rising noticeably and throughput flattening.

Spike Test: The sudden, extreme influx of 8,000 users in 1 second dramatically revealed the system's lack of resilience to abrupt traffic surges. The test resulted in a 100.00% failure rate and an APDEX of 0.000. The API immediately struggled, confirming that the system is not optimized for handling sudden, overwhelming traffic spikes, leading to immediate instability, connection timeouts, and connection reset errors.

# 8.0 Recommendations

Based on the test design and observations, the following recommendations can improve performance and stability for systems under similar load patterns:

1. Enable Auto-Scaling
Implement dynamic scaling for backend services to automatically handle sudden load spikes.

2. Optimize Database Queries
Slow queries significantly impact response time during heavy load. Indexing frequently accessed data and reducing query complexity can improve performance.

3. Implement Caching
Using in-memory caching (e.g., Redis, Cloudflare cache) reduces repeated database access and improves response consistency.

4. Apply Rate Limiting
Protects backend resources by limiting how many requests a single user or IP can send in each time.

5. Add Circuit Breaker
Helps prevent cascading failures by temporarily rejecting requests when the system is overloaded.

6. Improve Server Timeout and Queue Handling
Increasing server-side timeout thresholds and optimizing request queues can reduce dropped connections during load surges.

# 9.0 Conclusion

In conclusion, the comparison between Load, Stress, and Spike testing provides a complete view of how the DummyJSON API behaves under different levels of traffic intensity. Through Load Testing, the system demonstrated stable and predictable performance, maintaining fast response times and a low error rate. This shows that the API can support normal operating conditions without any noticeable degradation in user experience.
However, the Stress Test revealed the system’s performance boundaries. As the number of users increased beyond normal capacity, response times began to rise noticeably, throughput flattened, and intermittent errors started to appear. These results indicate that the system does not scale linearly under heavy traffic, and begins to encounter resource constraints such as network congestion, queue buildup, or limited backend processing capacity. Although the system remained partially operational during stress conditions, the increasing number of errors under prolonged heavy load highlights potential scalability limitations.

The Spike Test, on the other hand, produced the most dramatic results. When the number of users abruptly surged from low traffic to extremely high levels within one second, the API struggled to remain stable. Sharp increases in latency, connection timeouts, and connection reset errors were recorded almost immediately. This behaviour reflects the system’s limited ability to absorb sudden changes in concurrency. Such rapid surges can cause bottlenecks in server processing, network bandwidth, and request queuing, especially in environments that lack auto-scaling or are not optimized for sudden peak loads.

Overall, the combined results of all three tests show a clear picture of the system’s performance characteristics where it performs exceptionally well under normal load, begins to degrade under prolonged heavy load, and becomes unstable when subjected to sudden high traffic spikes. These findings not only identify the performance limits of the API but also highlight the specific conditions under which system reliability begins to decline. This information is crucial for predicting real-world behaviour, ensuring capacity planning, and identifying areas where performance improvements may be needed.

# Project Documentation

Final Report: https://github.com/nrnlfthh-cloud/Performance-Testing-using-Apache-JMeter/blob/9657d820ebdb26f16383468981f5153d0afb1bad/ITT440-NETWORK%20PROGRAMMING_INDIVIDUAL%20ASSIGNMENT%201%20(2023447786).pdf

Youtube Demonstration: https://youtu.be/bdqE2kc287A





