# 10hr Day - Deployment Guide

This guide will walk you through deploying your 10hr Day productivity tracker to Vercel with Supabase backend.

## Prerequisites

- A [Supabase](https://supabase.com) account
- A [Vercel](https://vercel.com) account
- A [GitHub](https://github.com) account
- Git installed on your machine

## Step 1: Set Up Supabase

### 1.1 Create a Supabase Project

1. Go to [https://supabase.com](https://supabase.com) and sign in
2. Click "New Project"
3. Fill in the project details:
   - **Project name**: `10hr-day` (or your preferred name)
   - **Database password**: Create a strong password (save this somewhere safe)
   - **Region**: Choose the closest region to your users
4. Click "Create new project" and wait for it to finish setting up (1-2 minutes)

### 1.2 Run Database Migrations

1. Once your project is ready, go to the **SQL Editor** in the left sidebar
2. Click "New query"
3. Copy the contents of `supabase/migrations/20260206151326_create_10hr_day_schema.sql`
4. Paste it into the SQL editor and click "Run"
5. Repeat for `supabase/migrations/20260206161320_update_rls_for_anonymous_auth.sql`

Your database schema is now set up with all the necessary tables and security policies.

### 1.3 Get Your Supabase Credentials

1. Go to **Project Settings** (gear icon in the left sidebar)
2. Click on **API** in the settings menu
3. You'll need two values:
   - **Project URL**: This is your `VITE_SUPABASE_URL`
   - **anon public** key: This is your `VITE_SUPABASE_ANON_KEY`
4. Keep this tab open or save these values somewhere safe

## Step 2: Push to GitHub

### 2.1 Initialize Git Repository

If you haven't already initialized a git repository:

```bash
git init
git add .
git commit -m "Initial commit - 10hr Day app"
```

### 2.2 Create GitHub Repository

1. Go to [https://github.com/new](https://github.com/new)
2. Create a new repository:
   - **Repository name**: `10hr-day` (or your preferred name)
   - **Visibility**: Choose Public or Private
   - **DO NOT** initialize with README, .gitignore, or license
3. Click "Create repository"

### 2.3 Push to GitHub

Follow the instructions shown on GitHub, or use these commands:

```bash
git remote add origin https://github.com/YOUR_USERNAME/10hr-day.git
git branch -M main
git push -u origin main
```

## Step 3: Deploy to Vercel

### 3.1 Import Project to Vercel

1. Go to [https://vercel.com](https://vercel.com) and sign in
2. Click "Add New..." and select "Project"
3. Click "Import" next to your GitHub repository
4. Vercel will detect that it's a Vite project automatically

### 3.2 Configure Environment Variables

Before deploying, you need to add your Supabase credentials:

1. In the "Configure Project" section, expand "Environment Variables"
2. Add the following variables:

   **Variable 1:**
   - Name: `VITE_SUPABASE_URL`
   - Value: [Your Supabase Project URL from Step 1.3]

   **Variable 2:**
   - Name: `VITE_SUPABASE_ANON_KEY`
   - Value: [Your Supabase anon public key from Step 1.3]

3. Click "Add" for each variable

### 3.3 Deploy

1. Click "Deploy"
2. Wait for the build to complete (usually 1-2 minutes)
3. Once deployed, click "Visit" to see your live app

## Step 4: Verify Everything Works

1. Visit your deployed app
2. Try adding a work session in the Track tab
3. Check that it appears in the month overview
4. Navigate to the Focus tab and add a goal
5. Check the Statistics tab to see your data

If everything works, congratulations! Your app is now live.

## Local Development

To run the project locally with your Supabase backend:

### 4.1 Create .env File

Create a `.env` file in the project root:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 4.2 Install Dependencies and Run

```bash
npm install
npm run dev
```

The app will be available at `http://localhost:5173`

## Updating Your Deployment

Whenever you make changes to your code:

```bash
git add .
git commit -m "Description of your changes"
git push
```

Vercel will automatically redeploy your app with the new changes.

## Troubleshooting

### Environment Variables Not Working

If your environment variables aren't being recognized:

1. Go to your Vercel project dashboard
2. Click "Settings" → "Environment Variables"
3. Verify the variables are set correctly
4. If you make changes, you need to redeploy:
   - Go to "Deployments"
   - Click the three dots on the latest deployment
   - Click "Redeploy"

### Database Connection Issues

If you're getting database errors:

1. Verify your Supabase project is active
2. Check that the environment variables match exactly
3. Make sure the migrations were run successfully
4. Check the Supabase logs in your project dashboard

### Build Failures

If the build fails on Vercel:

1. Check the build logs in the Vercel deployment page
2. Make sure all dependencies are in `package.json`
3. Test the build locally: `npm run build`

## Features

Your deployed app includes:

- **Track Tab**: Log deep work sessions with visual timeline
- **Focus Tab**: Set major and minor goals for each month
- **Statistics Tab**: View comprehensive analytics and performance metrics
- **Undo/Redo**: Undo or redo recent actions (located at top of Track tab)
- **Streak Tracking**: Automatic calculation of your work streak
- **Anonymous Auth**: Automatic user creation with Supabase

## Support

For issues or questions:

- Check the Supabase documentation: [https://supabase.com/docs](https://supabase.com/docs)
- Check the Vercel documentation: [https://vercel.com/docs](https://vercel.com/docs)
- Review the code in your repository

Happy tracking your deep work!
