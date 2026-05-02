# System Design

## Overview

League Stat-Us is designed as a league operations platform for recreational volleyball organizations. The system digitizes scheduling, scorekeeping, roster management, and analytics so that league organizers do not need to rely on paper records.

## Problem Statement

The league previously relied on pen-and-paper workflows for schedules, game results, and team performance records. This made information harder to update, search, share, and analyze.

## Goals

- Centralize schedules, scores, teams, and user profiles
- Support separate workflows for players, referees, and organizers
- Provide a responsive web interface usable from phones during games
- Store structured league data that can support future analytics
- Design for a user base of roughly 2,000-2,500 accounts

## High-Level Architecture

```text
[ Players / Referees / Admins ]
              |
              v
[ React Frontend - browser/mobile ]
              |
              v
[ Django REST API - application logic ]
              |
              v
[ PostgreSQL - users, teams, games, scores ]
              |
              v
[ Cloud hosting / backups ]
```

![System context diagram](assets/diagrams/context_diagram.png)

## User Roles

### Players

Players can view schedules, manage basic profile information, request team membership, and review team information.

### Referees

Referees can view assigned games, manage scorekeeping workflows, review rosters, and support game operations.

### Administrators / Organizers

Administrators can manage schedules, teams, users, referee assignments, and league operations.

## Design Decisions

### REST API Separation

The frontend and backend are separated through a REST API. This keeps the React interface independent from Django business logic and makes the system easier to expand or replace in pieces.

### Relational Database

Volleyball league data has natural relationships between users, teams, games, referees, schedules, and rankings. PostgreSQL was selected to model these relationships consistently.

### Role-Based Access

Different users need different privileges. Players should not have organizer-level access, referees need scorekeeping tools, and administrators need full league-management capabilities.

### Mobile-Friendly Web App

A web application avoids requiring users to install a separate mobile app while still supporting in-game access from phones and tablets.

## Use Cases

![Use case diagram](assets/diagrams/use_case_diagram.png)

Core use cases include:

- Player views schedule and team information
- Referee updates scores and game results
- Organizer creates schedules and assigns referees
- General user views public game information

## Scalability Considerations

The design targets a regional league environment with thousands of user accounts, frequent schedule updates, and modest database storage needs. The architecture can scale vertically on a cloud VM and later split services if traffic grows.

## Reliability Considerations

- Database backups should occur on a recurring schedule
- Critical errors should be logged and reviewed by administrators
- The system should recover before the next game window whenever possible
- Static documentation and operational runbooks should be kept with the repository
