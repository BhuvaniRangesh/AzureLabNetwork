# Azure Network Lab

## Lab Objective
- Create Hub and On-Prem VNets in Azure.
- Enable routing and inspection through a “fake NVA”.
- Connect On-Prem network to Hub via VPN.
- Test traffic routing, NSG rules, and connectivity.

## Lab Environment
- **On-Prem VM Public IP:** 20.106.208.29
- **Hub VM Private IP:** 10.0.2.4
- **Subnets:**
  - subnet-inspect (Hub)
  - subnet-nva (Hub, NVA simulated by Hub VM)
- **Route Table:** rtb-inspect
- **Routes configured:**
  1. Default outbound → Hub VM (10.0.2.4)
  2. Azure Storage bypass → Internet
  3. Local subnet bypass → Virtual Network
  4. Drop traffic to Spoke VNet → None

## Lab Steps
1. Created Resource Group and VNets
2. Created Hub VM, installed Nginx
3. Created On-Prem VM
4. Configured route table rtb-inspect and associated with subnet-inspect
5. Configured routes as above
6. SSH into On-Prem VM and validated connectivity:
   - Ping Hub VM: `ping 10.0.2.4`
   - Test HTTP: `curl -I http://10.0.2.4`
   - Test Internet: `curl -I https://www.google.com`
7. Verified Spoke route blocked (if Spoke VNet existed)

## Notes
- Free account limitation: No separate NVA or Spoke VM created.
- Hub VM acts as “fake NVA” for routing purposes.
- Lab demonstrates routing, peering, NSG rules, and outbound inspection logic.
