---
icon: users
description: Guide to registering and managing organizations on Kick for developers, including Drops, campaigns, and member management.
---

# Organization Management

## Introduction
Kick Organizations let you manage Drops campaigns, rewards, and members collaboratively. Organizations are ideal for teams or groups that want to coordinate developer activities, manage campaigns, and (soon) own OAuth apps together.

## When to Use Organizations
- Running Drops campaigns and rewards.
- Managing multiple members for developer access.
- (Coming soon) Managing OAuth apps as a group.

## Registration & Requirements
To register an organisation, email developers@kick.com with the following information:
  * Organisation Name.
  * Organization URL.
  * URL to your logo.
  * Stream category your organisation would like to claim.
  * Kick usernames of the members that belong to the organisation (including your own). Ensure they all have 2FA enabled
  * OAuth app client ID - this can be found by following the [App Setup guide](https://docs.kick.com/getting-started/kick-apps-setup).
  * Webhook URL - used to send [webhooks when a reward is claimed](#webhooks-for-drops).
  * Connection Page URL - the page used to connect users from your system to Kick.


## Approval Process
- After submitting, a Kick team member will review and create the organization.
- If more info is needed, the team will reach out.

## Roles & Permissions
- Only the Owner role exists for now.
- Owners can add/remove any user (including other owners), but cannot delete themselves.
- More roles will be added in the future.

## Managing Members
- New members are added via their username. They will need to have an account on Kick, with 2FA enabled before being added.
- Members can be removed by clicking on the 'Remove' button found on the Members page.

## FAQ / Troubleshooting
- For support, email developers@kick.com
- Reference related docs as needed (token generation, webhooks, etc.)

## References
- [Token Generation](../getting-started/generating-tokens-oauth2-flow.md)
- [Webhook Security](../events/webhook-security.md)
