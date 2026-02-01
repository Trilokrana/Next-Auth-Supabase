# Next.js Authentication System

A production-ready authentication system built with Next.js 16, Supabase Authentication, and Tailwind CSS. Features secure user signup, login, logout, and session-based route protection with a clean, modern UI.

## 🚀 Features

- ✅ **Email & Password Authentication** - Secure user registration and login
- ✅ **Session Management** - Persistent sessions across page reloads
- ✅ **Protected Routes** - Middleware-based route protection
- ✅ **Client & Server Validation** - Comprehensive form validation
- ✅ **Modern UI** - Clean, responsive design with Tailwind CSS
- ✅ **Production Ready** - Built with best practices and security in mind
- ✅ **TypeScript** - Fully typed for better development experience

## 📋 Prerequisites

Before you begin, ensure you have:

- Node.js 18+ installed
- A Supabase account (free tier works perfectly)
- Git installed on your machine

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd next-auth
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Supabase

1. Go to [supabase.com](https://supabase.com) and create a new project
2. Wait for the project to be fully set up
3. Go to **Settings** → **API**
4. Copy your **Project URL** and **anon/public key**

### 4. Configure Environment Variables

Create a `.env.local` file in the root directory:

```bash
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Replace the placeholder values with your actual Supabase credentials.

### 5. Configure Supabase Authentication

In your Supabase dashboard:

1. Go to **Authentication** → **Providers**
2. Enable **Email** provider
3. Configure email settings:
   - **Disable** email confirmation for development (optional)
   - Or configure SMTP for production email confirmations
4. Go to **Authentication** → **URL Configuration**
5. Add your site URL and redirect URLs:
   - Site URL: `http://localhost:3000` (development) or your production URL
   - Redirect URLs: Add `http://localhost:3000/auth/callback` and your production callback URL

### 6. Run the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 🏗️ Project Structure

```
next-auth/
├── app/
│   ├── dashboard/          # Protected dashboard page
│   │   └── page.tsx
│   ├── login/             # Login page
│   │   └── page.tsx
│   ├── signup/            # Signup page
│   │   └── page.tsx
│   ├── globals.css        # Global styles
│   ├── layout.tsx         # Root layout
│   └── page.tsx           # Home page
├── components/
│   └── LogoutButton.tsx   # Reusable logout component
├── lib/
│   └── supabase/
│       ├── client.ts      # Browser Supabase client
│       ├── server.ts      # Server Supabase client
│       └── middleware.ts  # Session management for middleware
├── middleware.ts          # Route protection middleware
├── .env.local            # Environment variables (not in git)
├── .env.example          # Example environment variables
├── package.json
└── README.md
```

## 🔐 Authentication Flow

### Signup Flow

1. User enters email and password on `/signup`
2. Client-side validation checks:
   - Valid email format
   - Password minimum length (6 characters)
   - Password confirmation matches
3. Supabase creates the user account
4. User is redirected to `/dashboard` after successful signup

### Login Flow

1. User enters credentials on `/login`
2. Client-side validation checks credentials format
3. Supabase authenticates the user
4. Session is created and stored in cookies
5. User is redirected to `/dashboard`

### Session Management

- Sessions persist across page reloads
- Middleware checks authentication on every request
- Protected routes redirect to `/login` if unauthenticated
- Auth pages (`/login`, `/signup`) redirect to `/dashboard` if already authenticated

### Logout Flow

1. User clicks logout button on dashboard
2. Supabase signs out the user
3. Session is cleared from cookies
4. User is redirected to `/login`

## 🛡️ Security Features

- **Server-Side Session Validation** - All protected routes validate sessions server-side
- **Middleware Protection** - Automatic route protection via Next.js middleware
- **Secure Cookie Storage** - Sessions stored in httpOnly cookies
- **Client & Server Validation** - Double validation for all user inputs
- **Environment Variables** - Sensitive keys never exposed to client
- **Password Requirements** - Minimum 6 characters enforced
- **Error Handling** - Graceful error messages without exposing system details

## 📱 Routes

### Public Routes
- `/` - Home page with links to login/signup
- `/login` - User login page
- `/signup` - User registration page

### Protected Routes
- `/dashboard` - User dashboard (requires authentication)

## 🎨 UI/UX Features

- **Responsive Design** - Works perfectly on mobile, tablet, and desktop
- **Loading States** - Visual feedback during async operations
- **Error Messages** - Clear, user-friendly error displays
- **Success Indicators** - Confirmation messages for successful actions
- **Form Validation** - Real-time validation feedback
- **Smooth Transitions** - Polished animations and transitions

## 🚀 Deployment

### Deploy to Vercel

1. **Push to GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

2. **Deploy on Vercel:**
   - Go to [vercel.com](https://vercel.com)
   - Import your GitHub repository
   - Configure environment variables:
     - `NEXT_PUBLIC_SUPABASE_URL`
     - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - Click **Deploy**

3. **Update Supabase URLs:**
   - Go to your Supabase dashboard
   - Navigate to **Authentication** → **URL Configuration**
   - Add your Vercel deployment URL to:
     - Site URL: `https://your-app.vercel.app`
     - Redirect URLs: `https://your-app.vercel.app/auth/callback`

## 🧪 Testing the Application

1. **Sign Up:**
   - Go to `/signup`
   - Enter a valid email and password
   - Verify successful account creation

2. **Login:**
   - Go to `/login`
   - Enter your credentials
   - Verify redirect to dashboard

3. **Protected Routes:**
   - Try accessing `/dashboard` without logging in
   - Verify redirect to `/login`

4. **Session Persistence:**
   - Log in and refresh the page
   - Verify you remain logged in

5. **Logout:**
   - Click logout button on dashboard
   - Verify redirect to login page
   - Try accessing `/dashboard` again
   - Verify redirect to login

## 🔧 Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `NEXT_PUBLIC_SUPABASE_URL` | Your Supabase project URL | Yes |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Your Supabase anonymous key | Yes |

## 📦 Tech Stack

- **Framework:** Next.js 16 (App Router)
- **Language:** TypeScript
- **Authentication:** Supabase Auth
- **Styling:** Tailwind CSS
- **Deployment:** Vercel
- **Version Control:** Git/GitHub

## 🐛 Troubleshooting

### "Invalid login credentials" error
- Verify the email and password are correct
- Check if email confirmation is required in Supabase settings

### Session not persisting
- Clear browser cookies and try again
- Verify environment variables are set correctly
- Check Supabase URL configuration includes your domain

### Redirect issues
- Ensure Site URL and Redirect URLs are configured in Supabase
- Verify middleware.ts is not excluded from your routes

### Build errors
- Run `npm install` to ensure all dependencies are installed
- Delete `.next` folder and rebuild
- Verify Node.js version is 18+

## 📄 License

MIT License - feel free to use this project for learning or production.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

## 👨‍💻 Author

Built with ❤️ using modern web technologies

## 🔗 Links

- **Live Demo:** [Your Vercel URL]
- **GitHub Repository:** [Your GitHub URL]
- **Supabase:** [supabase.com](https://supabase.com)
- **Next.js:** [nextjs.org](https://nextjs.org)

---

**Note:** This is a production-ready starter template. Feel free to customize and extend it based on your specific requirements.
