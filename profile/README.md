# ArenaRaid - Classic FPS Matchmaking Platform

A cloud-hosted matchmaking, lobby, and real-time communication platform built for legacy first-person shooter enthusiansts. ArenaRaid centralizes game-specific lobby discovery, player coordination, social features, and voice chat into a single unified application.

> **Oregon State CS46X - Talat Ali, Adam Boudraa, Scott Ladd**

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend API | ASP.NET Core (C#) |
| Authentication | ASP.NET Identity + JWT Bearer |
| Real-Time | ASP.NET SignalR |
| Voice Chat | WebRTC + MediaSoup SFU + Socket.IO (Node.js) |
| Primary Database | MySQL (Entity Framework Core, code-first) |
| Transient State | Redis (StackExchange.Redis) |
| Infrastructure | AWS ECS Fargate, RDS (multi-AZ), ALB |
| CI/CD | AWS CodePipeline + CodeBuild + ECR |
| IaC | AWS CDK |

---

## Features

- **User Accounts** - Register, log in, change email/password, and manage a personalized profile (bio, pronouns, avatar)
- **Game Lobbies** - Browse and join persistent, game-specific lobbies; create sub-rooms within lobbies for match organization
- **Real-Time Chat** - Live text chat within lobbies and rooms via SignalR with spam detection
- **Voice Chat** - Multi-party voice in rooms via WebRTC (MediaSoup SFU); mic mute/unmute, push-to-talk
- **Social Features** - Friend requests, friends list, online presence indicators, and direct messaging between friends
- **Role-Based Access** - JWT-protected endpoints; moderator-only actions enforced server-side

---

## Architecture Overview

- **Three data stores:** `IdentityContext` (user accounts/auth), `DataModelContext` (arenas, friends, profiles), and **Redis** (live presence, connections, active arena instances)
- **SignalR hubs:** `/chat` for lobby/room events and `/messengerhub` for DMs and friend notifications
- **Voice pipeline:** Socket.IO signaling service --> MediaSoup SFU --> WebRTC transports per participant
- **Cloud:** AWS ECS Fargate behind an Application Load Balancer; RDS MySQL multi-AZ for durability
