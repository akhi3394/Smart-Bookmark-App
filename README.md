# Smart Bookmark App

A real-time bookmark manager built with Next.js 14, Supabase, and Tailwind CSS.

## Features
- **Google Authentication**: Secure login without passwords.
- **Real-time Updates**: Bookmarks sync instantly across devices.
- **Privacy**: Row Level Security (RLS) ensures users only see their own bookmarks.
- **Responsive Design**: Premium glassmorphism UI.

## Setup Instructions

1.  **Clone the repo**.
2.  **Install dependencies**: `npm install`.
3.  **Environment Variables**:
    Create `.env.local` with:
    ```
    NEXT_PUBLIC_SUPABASE_URL=your_project_url
    NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key
    ```
4.  **Database Setup**:
    Run the SQL script in `database_schema.sql` in your Supabase SQL Editor to create the table and policies.
5.  **Run Locally**: `npm run dev`.

## Challenges & Solutions

### 1. NPM Naming Restrictions
**Problem**: The initial project folder `Abstrait_Assignement` contained capital letters, which `npm` does not allow for package names.
**Solution**: I scaffolded the app into a temporary directory `smart-bookmark-app` and then moved the files to the root directory.

### 2. Interactive CLI Prompts
**Problem**: The `create-next-app` command stalled because it was waiting for user input (React Compiler prompt), causing the automated process to hang.
**Solution**: I restarted the process with `CI=true` and the `--yes` flag to force non-interactive mode.

### 3. Real-time Subscription Types
**Problem**: Getting the correct types for Supabase Realtime payloads can be tricky.
**Solution**: I used a generic `postgres_changes` filter and manually cast the payload to the `Bookmark` interface for simplicity in this scope.

### 4. Middleware Session Management
**Problem**: Ensuring the Supabase session is updated on every request to prevent premature expiration.
**Solution**: Implemented a robust `updateSession` function in middleware that handles cookie management between the request and response.
