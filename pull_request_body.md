## Description
This PR implements admin mode with teacher authentication to resolve issue #5.

## Problem Solved
Students were removing each other from activities to free up space for themselves. This was causing conflicts and disrupting the integrity of the system.

## Changes Made

### Backend (`src/app.py`)
- Added session-based authentication system with in-memory storage
- Created login, logout, and session verification endpoints
- Protected signup and unregister endpoints - now require valid session token
- Added support for loading teacher credentials from JSON file

### Frontend
- **HTML**: Added user icon in header, login modal, and authentication status banner
- **JavaScript**: Implemented login/logout flow, session management with localStorage, and conditional UI based on auth state
- **CSS**: Styled user menu, dropdown, modal, and auth notices

### New File
- **`teachers.json`**: Stores teacher usernames and passwords (contains default admin and teacher1 accounts)

## How It Works

### For Students (Not Logged In)
- ✅ Can view all activities and participants
- ❌ Cannot register or unregister students
- See "Viewing mode" banner

### For Teachers (Logged In)
- ✅ Can view all activities and participants
- ✅ Can register students to activities
- ✅ Can unregister students from activities
- See "Teacher mode" banner
- Delete buttons (❌) appear next to each participant

## Testing
The login credentials are:
- Username: `admin` / Password: `admin123`
- Username: `teacher1` / Password: `password123`

## Security Notes
- Sessions are stored in-memory (will be lost on server restart)
- Passwords are currently stored in plaintext in `teachers.json`
- For production use, consider: password hashing, persistent session storage, and HTTPS

Fixes #5
