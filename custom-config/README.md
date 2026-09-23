# Custom LZA configuration

This directory is a deployable Landing Zone Accelerator configuration based on
the repository's default Universal Configuration baseline.

## Design

- Home region: `us-east-1`
- Accounts: Management, LogArchive, Audit, SharedServices, Network, and Perimeter
- IPAM root pool: `10.0.0.0/16`
- Transit Gateway owner: Network
- VPCs:
  - Network: `10.0.0.0/22`
  - SharedServices: `10.0.4.0/22`
  - Perimeter: `10.0.8.0/22`
- Each VPC receives two public and two private `/24` subnets across Availability
  Zones `a` and `b`.
- Each VPC has an internet gateway and one NAT Gateway in its public subnet in
  Availability Zone `a`.
- Both private subnets in each VPC are used for the Transit Gateway attachment.

Using one NAT Gateway per VPC reduces cost but makes private-subnet internet
egress dependent on Availability Zone `a`.

## Deployment

Copy the entire contents of this directory into the configuration repository
used by Landing Zone Accelerator. Keep the relative paths intact because the
YAML configuration references the included policy and automation files.

Before deployment, confirm that the configured plus-addressed email aliases are
accepted by the `slalom.com` mail system and are not already associated with AWS
accounts.
