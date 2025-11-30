# Audit Trail in a Sensitive Operations Platform

When building platforms that handle sensitive operations such as infrastructure provisioning, role management, or project automation, **visibility** is as crucial as **access control**.

<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="120" alt="Nest Logo" /></a>
</p>

[circleci-image]: https://img.shields.io/circleci/build/github/nestjs/nest/master?token=abc123def456
[circleci-url]: https://circleci.com/gh/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="_blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
<a href="https://circleci.com/gh/nestjs/nest" target="_blank"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg" alt="Donate us"/></a>
    <a href="https://opencollective.com/nest#sponsor"  target="_blank"><img src="https://img.shields.io/badge/Support%20us-Open%20Collective-41B883.svg" alt="Support us"></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow" alt="Follow us on Twitter"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Why Audit Trails?

With users managing organizations, projects, and cloud resources—often collaboratively—it's essential to answer questions like:
- **Who** created or modified a resource?
- **When** did the action happen?
- **What** changed?

## Audit Trail Goals

- **Automatic logging:** Every significant action triggers an audit log.
- **Comprehensive context:** Each log includes user, organization, and resource details.
- **Dedicated storage:** Logs are stored in a separate database table, enabling efficient querying and display.

## Architecture Overview

A typical flow for capturing audit information in the system:

```
Controller  
   ↓  
Service  
   ↓  
AuditService  
  ↘            ↘
AuditRepository  EventEmitter (async)
     (DB)
```

- **Direct Logging:** Actions record audit entries by calling `AuditService` directly.
- **Async Logging:** For non-blocking cases, actions emit audit events captured asynchronously.

## Example Scenario

Whenever a user creates, modifies, or deletes a resource (like a project or cloud resource), an audit record is created with:
- **User context:** Who made the change.
- **Organization context:** Under which organization the action happened.
- **Resource details:** What resource was affected and how.

## Implementation in NestJS

- **AuditService:** Offers methods to generate audit logs for operations.
- **AuditRepository:** Persists logs to a dedicated table.
- **EventEmitter:** Used for background/async logging, maintaining system performance.

## Querying & Display

Audit logs are easily queried to answer critical questions and support compliance needs.

This audit trail system ensures that every operation in your platform is traceable, improving transparency, accountability, and security.
