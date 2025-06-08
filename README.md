To setup first create a VirtioFS directory mapping within your Proxmox environment

*Datacenter -> Directory Mappings -> Add*

[Directory Mapping Setup Video](https://www.youtube.com/watch?v=d_zlMxkattE)
**Keep note of your directories path and the directory mapping name**


Within the noted directory path all your Docker Compose related files should be present (This is setup on your proxmox host machine)

*/DIRECTORY_PATH/docker-compose.yaml*

On your proxmox machine import the [deploy.sh](./Deploy.sh) script and open it in a text editor then change the `$VIRTIOFS` to your respective directory mapping name along with `$VMID`, `$STORAGE`, and CloudInit IP Configuration (Located Towards The Bottom) if needed

From here run the script and a CloudInit VM is created with the VirtioFS share mounted to /Docker along with the installation of docker and running `docker compose up -f /Docker/docker-compose.yaml up -d`

Remotely from the Proxmox host you can utilize the guest agent to push commands to the VM using the following command

`qm guest exec $VMID -- <COMMAND>`

Example: `qm guest exec $VMID -- docker compose -f /Docker/docker-compose.yaml up -d`
