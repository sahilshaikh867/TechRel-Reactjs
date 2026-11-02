# API Integration Lab — 10 Student Practical

## Scenario
You are a junior frontend developer. Build a customer dashboard.

## Tasks
1. Create the React app from scratch.
2. GET users from JSONPlaceholder.
3. Display name, username, email, phone, website and company.
4. Add search by name/email.
5. Create users with POST.
6. Edit users with PUT.
7. Delete users with DELETE.
8. Add GitHub username search.
9. Display GitHub avatar, name, followers, following, public repositories and profile link.
10. Test wrong URL, invalid username and offline network.
11. Refactor HTTP code into `src/services/api.js`.
12. Verify no private secret is committed.

## Bonus
- Pagination
- Debounced search
- AbortController
- Retry/backoff
- Toast notifications
- React Router
- Backend proxy

## Final question for the student
Explain this complete flow:

```text
User action
→ React event handler
→ API function
→ HTTP request
→ Server
→ JSON response
→ state update
→ React re-render
```
