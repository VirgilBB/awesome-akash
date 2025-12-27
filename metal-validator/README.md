# Metal Blockchain Validator

Deploy a Metal blockchain validator node on Akash Network with dedicated IP support for optimal P2P connectivity.

## Quick Start

### Prerequisites

- Akash wallet with AKT tokens
- Metal wallet with METAL tokens (minimum 1 METAL for testnet)
- Provider with `ip-lease: true` attribute (for dedicated IP)

### Deploy via Akash Console

1. Go to [Akash Console](https://console.akash.network/)
2. Click "Deploy" → "Upload SDL"
3. Upload this `deploy.yaml` file
4. Choose a provider with `ip-lease: true` attribute
5. Deploy and wait 5-10 minutes for bootstrap

### Two-Step Deployment Process

**Important:** This template requires a two-step deployment:

1. **Deploy first** - Create deployment to get LoadBalancer IP assigned
2. **Get IP** - Check Akash Console → Deployment → "IP(s)" field
3. **Update deployment** - Set `METAL_PUBLIC_IP=<your-loadbalancer-ip>` in Environment Variables
4. **Use final Node ID** - Copy Node ID from logs AFTER the update completes

**Why two steps?** The LoadBalancer IP is assigned AFTER deployment, so we need to update with the correct IP.

## What You Get

After deployment, check your logs for validator setup data:

```
========================================
=== METAL TESTNET VALIDATOR SETUP DATA ===
========================================

Node ID
NodeID-ABC123...

Proof of Possession - Public Key
0x3059301306...

Proof of Possession - Signature
0x3045022100...

========================================
=== NETWORK STATUS ===
========================================
Public IP: 62.3.50.131
Connected Peers: 20+
Network: Metal Testnet (Tahoe)
```

Copy this data to register your validator on the [Metal Dashboard](https://metalblockchain.org/validators).

## Features

- **Dedicated IP Support**: Uses Akash IP leases for optimal P2P connectivity
- **Advanced IP Detection**: Multi-method IP detection (Kubernetes API → Environment Variables → External Services)
- **Manual IP Override**: Set `METAL_PUBLIC_IP` environment variable if auto-detection fails
- **File Descriptor Limits**: Increased to 65536 to prevent "too many open files" errors
- **Peer Monitoring**: Real-time peer count monitoring every 5 minutes
- **Bootstrap Detection**: Waits for blockchain to fully bootstrap before reporting success

## Configuration

### Environment Variables

- `METAL_PUBLIC_IP` (optional): Manually set your LoadBalancer IP if auto-detection fails
  - Get IP from: Akash Console → Deployment → "IP(s)" field
  - Set in: Akash Console → Deployment → Environment Variables

### Mainnet Deployment

For mainnet deployment, see the [full repository](https://github.com/VirgilBB/metal-validator-akash) for `deploy-mainnet.yml`.

## Cost

- **Testnet**: Approximately $2-5/month on Akash Network
- **Mainnet**: Approximately $5-15/month on Akash Network
- Varies by provider and market conditions

## Resources

- [Metal Blockchain](https://metalblockchain.org/)
- [Metal Testnet Explorer](https://tahoe-explorer.metalblockchain.org/validators)
- [Metal Mainnet Explorer](https://explorer.metalblockchain.org/validators)
- [Metal Testnet Faucet](https://faucet.metalblockchain.org/)
- [Metal Validator Dashboard](https://metalblockchain.org/validators)
- [Full Documentation & Tutorials](https://github.com/VirgilBB/metal-validator-akash)

## Troubleshooting

### Node shows "Not connected" in explorer

**Solution**: Complete the two-step deployment process. Set `METAL_PUBLIC_IP` to your LoadBalancer IP from Akash Console and update the deployment.

### 0 peers connected

**Solution**: Ensure you completed the two-step process and set the correct LoadBalancer IP in `METAL_PUBLIC_IP`.

### Initial Node ID changes after update

**Solution**: This is normal. Use the final Node ID from logs AFTER the IP update completes.

## Need Help?

- **Issues?** Open an issue in the [repository](https://github.com/VirgilBB/metal-validator-akash)
- **Questions?** Join [Akash Discord](https://discord.akash.network/)
- **Metal Support?** Join [Metal Discord](https://discord.gg/metalblockchain)

---

**Version**: v2.5 | **MetalGo**: v1.12.0-hotfix | **Network**: Testnet (Tahoe)

