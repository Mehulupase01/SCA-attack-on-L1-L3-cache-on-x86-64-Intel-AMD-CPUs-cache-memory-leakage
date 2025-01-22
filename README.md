# Side Channel Attack on L1 & L3 cache of x86-64 Intel / AMD CPUs using Cache access patterns & Memory leakage using MASTIK
 This project explores the vulnerability of cryptographic algorithms AES and RSA to micro-architectural side-channel attacks using the MASTIK toolkit. By employing the Prime+Probe technique, the project analyzes cache access patterns and memory leakage on Intel and AMD systems, highlighting potential security risks in cryptographic implementations

## Description
This project explores the vulnerability of cryptographic algorithms AES and RSA to micro-architectural side-channel attacks using the MASTIK toolkit. By employing the Prime+Probe technique, the project analyzes cache access patterns and memory leakage on Intel and AMD systems, highlighting potential security risks in cryptographic implementations.

## Task / Problem Statement
This project investigates the feasibility and impact of micro-architectural side-channel attacks on AES and RSA implementations. Specifically, it leverages MASTIK to analyze how cache-based side-channel vulnerabilities can be exploited using the Prime+Probe technique. The task also involves extending previous work to study how MASTIK behaves on AMD systems.

## Sub-Tasks
1. **Setup MASTIK on Intel and AMD systems**: Configure the MASTIK toolkit for both Intel and AMD processors.
2. **Implement AES and RSA cryptographic algorithms**: Test the impact of cache-based side-channel attacks on AES and RSA implementations.
3. **Conduct Prime+Probe attack**: Perform the attack to deduce memory access patterns from cache behavior.
4. **Data analysis and visualization**: Analyze the collected cache timing data and visualize it as heatmaps and memory access patterns.
5. **Compare results across Intel and AMD systems**: Assess the differences in cache leakage between the two processor architectures.
6. **Evaluate countermeasures**: Explore potential mitigations such as cache partitioning, randomization, and noise injection.

## Implementation Details
### 1. **System Setup and Configuration**
   - **Intel Systems**: MASTIK was configured to monitor L1 and L3 caches.
   - **AMD Systems**: Due to tool limitations, only L1 cache access was monitored on AMD systems.
   - **Virtualized Environment**: Tests on virtualized AMD systems were also conducted but faced challenges due to added noise.

### 2. **Prime+Probe Technique**
   - The Prime+Probe technique was employed to exploit cache-based side-channel vulnerabilities. In this method, the attacker populates the cache and then probes it to measure cache response times. Variations in timing data reveal memory access patterns, which could leak sensitive cryptographic information.

### 3. **Data Collection and Visualization**
   - Cache timing data was collected at high resolution, and visualized using heatmaps and memory access maps. These visualizations helped identify cache contention and potential vulnerabilities in the cryptographic operations.

### 4. **RSA and AES Encryption Experiments**
   - **AES on Intel Systems**: Various AES encryption experiments were conducted to examine cache access patterns in both L1 and L3 caches.
   - **RSA on Intel Systems**: RSA encryption experiments focused on cache access during modular exponentiation.
   - **AMD Systems**: Despite the tool's limitations, cache access patterns in L1 cache on AMD systems were also observed.

## Goals
- **Primary Goal**: Analyze the vulnerability of AES and RSA cryptographic implementations to cache-based side-channel attacks using MASTIK.
- **Secondary Goals**: 
  - Understand the feasibility of side-channel attacks across different processor architectures.
  - Extend MASTIK’s support for AMD systems.
  - Provide insights into potential mitigation strategies.

## Results
- **AES on Intel**: Cache-based leakage was observed in both L1 and L3 caches, with distinct heatmaps revealing memory access patterns.
- **RSA on Intel**: Cache access during RSA operations showed patterns that could potentially leak information about the private key.
- **AMD Systems**: Limited access to L1 cache on AMD systems revealed observable cache activity, despite the limitations of MASTIK.

## Algorithms Used
- **Prime+Probe**: This technique monitors cache access patterns by populating the cache and measuring response times to infer memory accesses. It’s an effective tool for side-channel attacks.
- **Flush+Reload and Evict+Reload**: Although not tested in this project, these techniques are often used to detect memory access patterns, especially in cryptographic workloads.

### Mathematical Equations
- **Prime+Probe Timing Equation**: The timing measurements obtained during the probe phase are compared against baseline values to identify differences indicating cache access:
  \[
  \text{Access Time} = \text{Probe Time} - \text{Baseline Time}
  \]
- **Cache Hit and Miss Patterns**: The success of side-channel attacks often depends on the ability to distinguish cache hits from misses, which is directly related to access time.

## Challenges and Limitations
- **AMD System Support**: MASTIK’s limited support for AMD processors meant that experiments could only be conducted on L1 cache, with no access to higher-level caches like L3.
- **Virtualization Noise**: Running experiments on virtualized AMD systems introduced noise, affecting the precision of cache timing measurements.

## Future Work
- Extend MASTIK’s support for AMD systems, particularly for monitoring L3 cache.
- Explore additional countermeasures to mitigate the risks posed by cache-based side-channel attacks.

## Countermeasures
1. **Cache Partitioning**: Allocate specific cache areas to processes to prevent shared access.
2. **Randomization**: Randomize cache access patterns to make it harder for attackers to predict memory access behavior.
3. **Noise Injection**: Introduce random delays to obfuscate cache timing measurements.
4. **Hardware Solutions**: Implement hardware-based solutions like Intel’s Cache Allocation Technology (CAT) to reduce the risk of cache leakage.

## References
- **MASTIK GitHub Repository**: [Mastik GitHub](https://github.com/0xADE1A1DE/Mastik)
- **Relevant Papers**:
  - "Cache Attacks and Countermeasures: The Case of AES" by Osvik et al. (2006)
  - "Flush+Reload: A High Resolution, Low Noise, L3 Cache Side-Channel Attack" by Yarom and Falkner (2014)

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/side-channel-attacks.git
   cd side-channel-attacks
   ```
2. Install dependencies:
   ```bash
   sudo apt-get install binutils-dev libdwarf-dev libelf-dev
   ```
3. Build the project:
   ```bash
   make
   ```
4. Run the experiments:
   ```bash
   ./run_experiments.sh
   ```

