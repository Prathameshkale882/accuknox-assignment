import psutil
import logging
from datetime import datetime

# Setup logging to a file
logging.basicConfig(filename='system_health.log', level=logging.INFO, format='%(asctime)s - %(message)s')

# Define threshold values
CPU_THRESHOLD = 80  # CPU usage percentage
MEMORY_THRESHOLD = 80  # Memory usage percentage
DISK_THRESHOLD = 80  # Disk usage percentage

def check_cpu():
    cpu_usage = psutil.cpu_percent(interval=1)
    if cpu_usage > CPU_THRESHOLD:
        logging.info(f"High CPU usage detected: {cpu_usage}%")
    return cpu_usage

def check_memory():
    memory_usage = psutil.virtual_memory().percent
    if memory_usage > MEMORY_THRESHOLD:
        logging.info(f"High memory usage detected: {memory_usage}%")
    return memory_usage

def check_disk():
    disk_usage = psutil.disk_usage('/').percent
    if disk_usage > DISK_THRESHOLD:
        logging.info(f"High disk usage detected: {disk_usage}%")
    return disk_usage

def monitor_system():
    cpu = check_cpu()
    memory = check_memory()
    disk = check_disk()
    print(f"CPU Usage: {cpu}% | Memory Usage: {memory}% | Disk Usage: {disk}%")

# Run monitoring
if __name__ == "__main__":
    monitor_system()
