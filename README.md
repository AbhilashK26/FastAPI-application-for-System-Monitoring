# Remote_system_monitoring_with_FastAPI_and_Pinggy
Here we have written FastAPI applications to monitor our system's performance- specifically CPU, RAM, Memory, and Disk usage.
We will see how to run these files locally and later we will mention how we can monitor remotely using Pinggy.

## Running a FastAPI server on localhost
### Step 1: Create a Virtual Environment

When you work in Python projects you should use a virtual environment (or a similar mechanism) to isolate the packages you install for each project.

To create a virtual environment, you can use the `venv` module that comes with Python.


```bash
python -m venv .venv
```

> Note: If the command `python` does not work, try replacing it with `python3`


That command creates a new virtual environment in a directory called `.venv`.

### Step 2: Activate the Virtual Environment

Activate the new virtual environment so that any Python command you run or package you install uses it.

#### For Linux, MacOS

```bash
source .venv/bin/activate
```

#### For Windows Powershell

```ps
.venv\Scripts\Activate.ps1
```

#### For Windows Bash

```bash
source .venv/Scripts/activate
```

Upgrading `pip` before installing packages like FastAPI is generally a good practice, especially if you're working in a new environment or haven't updated `pip` in a while.

To upgrade `pip`, use:

```bash
python -m pip install --upgrade pip
```

### Step 3: Install packages included in requirements.txt

To install packages included in requirements.txt, run the following command:-

```bash
pip install -r requirements.txt
```

### Step 4: Run the FastAPI Application

Now, you can run the application with the following command:

```bash
fastapi dev main.py
```

### Step 6: Check the output

Add the required endpoint with `http://127.0.0.1:8000` (example- `http://127.0.0.1:8000/cpu`)and open it in your browser.
You will see the expected JSON response.

#### Routes to monitor various aspects of CPU

1. `/cpu`: Get the overall CPU usage percentage.
2. `/cpu/cores`: Get the CPU usage for each core individually.
3. `/cpu/frequency`: Retrieve information about the current, minimum, and maximum CPU frequencies.

####  Routes to monitor Memory Usage

1. `/memory`: Get the current status of virtual memory.
2. `/memory/swap`: Retrieve swap memory usage statistics.

#### Routes to monitor RAM Usage

1. `/ram`: Returns RAM usage in percentage.

#### Routes to monitor Disk Usage

1. `/disk`: Returns overall disk usage for the root filesystem.
2. `/disk/partitions`: Provides information about mounted disk partitions.
3. `/disk/io`: Displays disk I/O statistics.

## Remotely Monitoring your FastAPI app through Pinggy

[Pinggy](https://pinggy.io) offers an easy and secure way to expose a local FastAPI application to the internet without needing complex server setups or cloud deployments.

Use the following command to set up a tunnel to your local development server:


```bash
ssh -p 443 -R0:localhost:8000 qr@a.pinggy.io
```


{{< pinggytunnel box="true" tunnelstring="Paste this command to start a tunnel to FastAPI:" portstring="FastAPI Port" localport="8000" webdebugenabled=false keepalive=true >}}
{{< /pinggytunnel >}}

Note: Replace the port 8000 in the command with the port where your local development server is running.

After running the command, Pinggy will generate a public URL which might looks like this:
```
http://rnnex-2405-201-800b-489d-7063-516b-6c80-5d24.a.free.pinggy.link
```

> Add the endpoint after this link to get the required output.
> Say for getting cpu uage informtion, the link would be like
```
http://rnnex-2405-201-800b-489d-7063-516b-6c80-5d24.a.free.pinggy.link/cpu
```

{{< image "system_monitoring_fastapi/pinggy_command_img.webp" "Pinggy command" >}}

When you paste the modified URL into your browser, your FastAPI application will process the request and return the output in JSON format, which will be displayed directly in the browser.

Output would look like:-

{{< image "system_monitoring_fastapi/pinggy_output.webp" "Output through Pinggy" >}}

## Advantages of Using Pinggy for Hosting FastAPI

Pinggy provides several unique benefits for developers:

1. **Quick Setup**: Instantly expose a local FastAPI app to the internet without configuring cloud infrastructure or deploying a server.
2. **Testing and Demos**: Ideal for sharing applications during development or conducting live demos. It simplifies the process of testing integrations with external services that require a public URL (e.g., webhooks, payment gateways).
3. **Flexible Access**: With Pinggy’s public URL, you can let others access your local application without being on the same network.
4. **Security Built-In**: Pinggy supports HTTPS by default, which helps secure the connection between clients and your local application.
5. **Developer-Friendly**: Pinggy is straightforward and doesn’t require heavy configurations, making it accessible for both new and experienced developers.
