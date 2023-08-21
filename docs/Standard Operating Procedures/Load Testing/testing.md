# Stress Testing 
>💡** Simulating stress test** of 5000 Users

## Introduction
Load testing evaluates application performance under expected user loads. This guide outlines load testing with 5000 users using Locust, including multiple endpoints and graph generation.

## Prerequisites:
1. Python 3.8 or later.
2. Locust. Follow [**Guide here**](./setup.md)

## Load Testing Setup:
1. Create `load_test.py`.
2. Define user behavior with `HttpUser` class and tasks.
3. Set user count and hatch rate in Locust web interface.

## Script:

This script here is for reference. Actual script will be shared to testing team.

```python
from locust import HttpUser, task, between
import pandas as pd
import matplotlib.pyplot as plt

response_times = []

class MyUser(HttpUser):
    wait_time = between(1, 5)
    
    @task
    def hit_endpoint1(self):
        response = self.client.get("/endpoint1")
        response_times.append(response.elapsed.total_seconds() * 1000)
        
    @task
    def hit_endpoint2(self):
        response = self.client.get("/endpoint2")
        response_times.append(response.elapsed.total_seconds() * 1000)
        
    # Add more @task methods for endpoints

# Access web interface: http://localhost:8089

# Save response times to a CSV file
data = pd.DataFrame(response_times, columns=['ResponseTime'])
data.to_csv('response_times.csv', index=False)

```

## Running the Load Test:
1. Open terminal/command prompt.
2. Navigate to script location: `cd path/to/script`.
3. Run Locust: `locust -f load_test.py`.
5. Configure user count, hatch rate, and start the test.


# Access web interface:
>💡**Click** [**View Graph**](http://localhost:8089) to view the real-time graph, or access the graph here: `http://localhost:8089`


## Graph Generation and Reporting:
1. After load test, open terminal.
2. Run graph script: `python graph.py`.



```python
# graph.py
import pandas as pd
import matplotlib.pyplot as plt
import uuid

# Load response times from the CSV file
data = pd.read_csv('response_times.csv')
response_times = data['ResponseTime'].tolist()

# Generate a graph using matplotlib and save it with a random file name
file_name = f'response_time_histogram_{uuid.uuid4()}.png'
plt.figure(figsize=(10, 6))
plt.hist(response_times, bins=20, color='blue', alpha=0.7)
plt.xlabel('Response Time (ms)')
plt.ylabel('Frequency')
plt.title('Distribution of Response Times')
plt.grid(True)
plt.savefig(file_name)  # Save the graph with the random file name

```

Access the graph `png` that will be saved to local machine.

##  Conclusion:
Locust enables in-depth load testing with multiple endpoints. Monitor real-time metrics and generate custom graphs for performance optimization insights.