# capturenetworktraffic
this is a python script that captures network traffic on your machine


code begins below



import os
import socket
import time

def main():
    # Open the log file in write mode
    with open("network_traffic.log", "w") as log_file:
        # Continuously capture network traffic
        while True:
            # Get a list of all open connections
            conn_list = os.popen("netstat -an").readlines()

            # Iterate through the connections
            for conn in conn_list:
                # Split the line into columns
                cols = conn.split()

                # Get the local and remote IP addresses and port numbers
                local_ip, local_port = cols[3].split(":")
                remote_ip, remote_port = cols[4].split(":")

                # Get the protocol (TCP or UDP)
                protocol = cols[0]

                # Get the connection state
                state = cols[5]

                # Write the connection info to the log file
                log_file.write(f"{time.ctime()}: {local_ip}:{local_port} {protocol} {remote_ip}:{remote_port} {state}\n")

            # Sleep for 1 second before capturing the next batch of traffic
            time.sleep(1)

if __name__ == "__main__":
    main()
