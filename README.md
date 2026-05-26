# React Hook Form + TanStack Query Profile System

## Project Overview

This project demonstrates the integration of React Hook Form with TanStack Query (React Query) and JSON Server to create a fully functional profile management system using a mock REST API.

The application separates client-side form state from server-side data management, following modern enterprise React architecture practices.

The system fetches user profile data from a mock REST API, hydrates the form using React Hook Form, supports profile updates through server mutations, performs cache invalidation, and maps simulated backend validation errors directly into the user interface.

---

# Features

- Fetch profile data using `useQuery`
- Update profile data using `useMutation`
- JSON Server mock REST API
- Cache invalidation with `invalidateQueries`
- Form hydration using `reset()`
- Server-side error handling using `setError()`
- Loading state management
- Dirty state tracking with `isDirty`
- Disabled save button until changes are made
- Simulated backend email conflict validation

---

# Technologies Used

- React
- Vite
- React Hook Form
- TanStack Query (React Query)
- Axios
- JSON Server
- JavaScript
- HTML/CSS

---

# External Infrastructure Setup

A local mock REST API was created using JSON Server.

The application stores profile data under the following endpoint:

```text
http://localhost:3001/profile
```

---

# Database Structure

```json
{
  "profile": {
    "username": "Paulina",
    "email": "paulina@example.com",
    "bio": "UX Designer and Application Development student.",
    "notifications": true
  }
}
```

---

# Core Functionalities

## Data Querying Phase — useQuery()

The application uses TanStack Query’s `useQuery()` hook to fetch profile data from:

```text
http://localhost:3001/profile
```

Query Key:

```javascript
["userProfile"]
```

### Implemented Features

- Loading state while fetching server data
- Automatic form hydration using `reset(data)`
- Declarative side-effect synchronization with `useEffect()`

---

## Data Mutation Phase — useMutation()

The application updates server data using TanStack Query’s `useMutation()` hook and HTTP PUT requests.

### Implemented Features

- PUT request mutation
- Cache invalidation using:

```javascript
queryClient.invalidateQueries({
  queryKey: ["userProfile"],
});
```

- Form state reset after successful mutation using:

```javascript
reset(updatedData)
```

---

## Form State Interlocking — isDirty

The Save button remains disabled when:
- no changes have been made
- mutation requests are pending

Implementation:

```javascript
disabled={!isDirty || mutation.isPending}
```

---

## Server Error Mapping

The application simulates a backend validation collision.

If the user enters:

```text
conflict@example.com
```

the mutation intentionally rejects the request and maps the error directly into the email field using:

```javascript
setError("email", {
  type: "server",
  message: "Email already exists",
});
```

---

# Installation Instructions

## Clone Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

---

## Navigate Into Project

```bash
cd react-query-profile-form
```

---

## Install Dependencies

```bash
npm install
```

---

# Required Dependencies

```bash
npm install react-hook-form
npm install @tanstack/react-query
npm install axios
npm install json-server@0.17.4
```

---

# Run JSON Server

Open terminal #1:

```bash
npm run server
```

JSON Server runs at:

```text
http://localhost:3001/profile
```

---

# Run React Application

Open terminal #2:

```bash
npm run dev
```

Vite runs at:

```text
http://localhost:5175
```

---

# Test Cases

## Normal Test Cases

### 1. Successful Profile Fetch
- Verify profile data loads automatically from JSON Server.

### 2. Successful Profile Update
- Modify profile information and save changes successfully.

### 3. Cache Invalidation
- Verify updated data persists after page refresh.

---

# Edge Test Cases

### 1. Invalid Email Format
- Enter invalid email structure and verify validation message appears.

### 2. Empty Username
- Remove username and verify required validation triggers.

### 3. Simulated Backend Conflict
- Enter:

```text
conflict@example.com
```

- Verify backend validation error displays:
  
```text
Email already exists
```

---

# Time and Space Considerations

## React Hook Form
React Hook Form minimizes unnecessary component re-renders by using uncontrolled inputs and internal subscriptions.

## TanStack Query
TanStack Query optimizes:
- data fetching
- caching
- server synchronization
- mutation handling

This architecture reduces redundant network requests and improves performance.

---

# Assignment Concepts Demonstrated

- `useQuery()`
- `useMutation()`
- `invalidateQueries()`
- `reset()`
- `setError()`
- `isDirty`
- `isPending`
- Server-state management
- Form-state management
- REST API integration

---

# Project Structure

```text
react-query-profile-form/
│
├── db.json
├── package.json
├── README.md
├── src/
│   ├── App.jsx
│   └── main.jsx
```
