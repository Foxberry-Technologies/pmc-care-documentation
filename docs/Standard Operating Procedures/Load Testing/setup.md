# Setup Locust on Windows

This document provides a step-by-step guide to installing and setting up Locust, a Python-based load testing tool, on a Windows operating system. Follow these instructions to ensure a successful installation and configuration.

## Prerequisites

Before you begin, make sure you have the following prerequisites in place:

- Windows operating system (Windows 7 or later)
- Internet connection

## Installation Steps

### 1. Install Python 3.8

Locust requires Python to be installed on your system. Here's how you can install Python 3.8:

1. Visit the official Python website: [Python Downloads](https://www.python.org/downloads/).
2. Download the latest version of Python 3.8 for Windows.
3. Run the installer. **Important:** Ensure that you select the "Add Python 3.8 to PATH" option on the first screen of the installer. This will add Python to your system's PATH environment variable, allowing you to easily run Python commands from the command line.

### 2. Install Visual Studio Build Tools

Locust has dependencies that require the Visual Studio Build Tools to be installed. Follow these steps to install the necessary tools:

1. Visit the Visual Studio Build Tools download page: [Visual Studio Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/).
2. Download and run the Visual Studio Build Tools installer.
3. Follow the on-screen instructions to install the required tools. You can choose the default installation options.

### 3. Install Required Python Packages

To run Locust, you need to install several Python packages. Open the Command Prompt (CMD) and execute the following commands:

a. Install pyzmq:
   ```
   pip install pyzmq
   ```

b. Install gevent:
   ```
   pip install gevent
   ```

c. Install greenlet:
   ```
   pip install greenlet
   ```

d. Install Locust:
   ```
   pip install locust
   ```

### 4. Verify Installation

After installing the required packages, ensure that everything is set up correctly by running a simple command:

1. Close the current instance of the Command Prompt to refresh environment variables.
2. Open a new instance of the Command Prompt.
3. Run the following command to verify Locust installation:
   ```
   locust --help
   ```

If the installation was successful, you should see the Locust help information displayed in the Command Prompt.

## Conclusion

Congratulations! You have successfully set up Locust on your Windows system. You can now use Locust to perform load testing and measure the performance of your applications. Refer to the [Locust Documentation](https://docs.locust.io/) for more information on how to create and run load tests using Locust.