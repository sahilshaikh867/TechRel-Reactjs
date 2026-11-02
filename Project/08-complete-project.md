# API Integration Lab — 08 Complete Project

## Project: User & Developer Dashboard

### Features
1. Load users
2. Search users
3. Display user cards
4. Create a user
5. Update a user
6. Delete a user
7. Search a GitHub profile
8. Loading/error/empty states
9. Central API service
10. Environment configuration

## Build order
### Phase 1
Create static React UI.

### Phase 2
Implement GET users.

### Phase 3
Add loading/error/empty states.

### Phase 4
Add local search.

### Phase 5
Add POST form.

### Phase 6
Add PUT and DELETE.

### Phase 7
Add GitHub integration.

### Phase 8
Move all HTTP calls to `src/services/api.js`.

### Phase 9
Add `.env` for public configuration.

### Phase 10
Test failures and inspect Network tab.

## Final architecture
```text
App
├── UserList
│   └── UserCard
├── CreateUserForm
└── GithubProfile

services/
└── api.js
```
