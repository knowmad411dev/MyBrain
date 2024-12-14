---
tags: 
- cloud
video-url: https://www.youtube.com/watch?v=D-KHaXNmpiI&list=WL&index=28
---

## **VPN Build**

### Overview

The creator of the guide shares their experience of deploying a VPN server to tunnel their internet connection through different regions, particularly to access geo-blocked content. Instead of paying for a VPN service, they demonstrate how to build one using Algo VPN, Docker, and AWS for minimal costs. The guide focuses on security, cost reduction, and automation.

### Step-by-Step Instructions

1. **Set Up Algo VPN on [[Docker]]:**

    - Algo VPN is a popular open-source project sponsored by Trail of Bits. It uses Ansible and offers strong encryption.
    - The setup process runs inside a Docker container to maintain a clean environment. Algo VPN can be deployed on multiple platforms such as AWS, Google Cloud, Azure, or Hetzner (recommended for cost-efficiency).
    - Use a pre-configured `config.cfg` file, which is a duplicate of the one available in the Algo project on GitHub.
    - Run the following Docker command to start the process:

        ```
        docker run --cap-drop=all -it -v $(pwd)/config.cfg:/algo/config.cfg algo
        ```

    - This command includes flags like `--cap-drop=all` for limiting security capabilities inside the container and `-v` to mount a volume with the configuration file.
    - Once the Docker command runs, you’ll be presented with interactive questions to select the platform and provide cloud credentials.

2. **Deploy on AWS:**

    - For AWS, ensure you have cloud credentials set up. If not, follow AWS documentation to configure them.
    - Choose the region (e.g., Tokyo for Japanese content) and the instance type (e.g., T3.micro for cost-efficiency).
    - Monitor the deployment through AWS CloudFormation, which is similar to Terraform for Infrastructure-as-Code.
    - Once the instance is running, you'll find the public IP address and other details in the AWS console.

3. **WireGuard Configuration:**

    - After the deployment, Algo generates VPN profiles that can be loaded into the WireGuard client.
    - WireGuard is an open-source VPN client that supports multiple platforms (Windows, macOS, Linux, iOS, etc.).
    - Import the profile into WireGuard and activate it to establish a secure VPN connection.

4. **Cost Management:**

    - A T3.micro instance in Tokyo costs around $7.50/month if running constantly. However, by stopping the instance when not in use, the cost can be reduced to nearly zero.
    - Use the following AWS CLI commands to stop and start the instance as needed:
        - To stop the instance:

            ```
            aws ec2 stop-instances --instance-ids <instance-id> --region <region>
            ```

        - To start the instance:

            ```
            aws ec2 start-instances --instance-ids <instance-id> --region <region>
            ```

    - To avoid additional charges, always delete the CloudFormation stack if you're no longer using the instance. Deleting only the EC2 instance leaves residual resources (e.g., public IP address, storage) that still incur costs.

5. **Advanced Automation:**

    - For easier management and automation, create scripts to start and stop the instance without accessing the AWS console every time.
    - Example: Use `jq` to filter out the instance ID and automate the stop/start process using shell scripts.

6. **Zero Trust Alternatives:**

    - Although VPNs are effective, modern security trends lean toward Zero Trust solutions for accessing internal networks.
    - Twingate (a sponsor of the video) offers a Zero Trust solution that allows secure, remote access to private resources without the need for a VPN.

### Tools & Technologies Used

- **Algo VPN**: Open-source VPN deployment tool.
- **Docker**: Containerization platform used to run Algo VPN in a clean environment.
- **AWS**: Cloud platform used to host the VPN server.
- **WireGuard**: VPN client used to connect to the deployed VPN server.
- **Twingate**: A Zero Trust solution for secure access (optional, sponsor mentioned).

### Websites & Resources

- **Algo VPN GitHub**: [Algo GitHub Project](https://github.com/trailofbits/algo)
- **AWS CloudFormation Documentation**: [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
- **WireGuard VPN Client**: [WireGuard](https://www.wireguard.com/)
- **Twingate**: [Twingate Website](https://twingate.com)

The guide concludes by suggesting ways to avoid losing terminal commands by using an open-source tool to maintain command history, hinting at more content in future videos.

### Final Thoughts

By following the provided instructions and using tools like AWS, Docker, and Algo VPN, you can set up your own VPN server securely, automate the process, and minimize costs.

[[Cloud]]  [[AWS EC2]]