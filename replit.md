# TrustTether

An on-chain social feed platform built on the HeLa blockchain where every interaction (post, like, comment, tip) is recorded on-chain with content stored on IPFS.

## Overview

TrustTether is a decentralized social media platform that combines blockchain transparency with modern UX. Users connect their MetaMask wallets to create posts, interact with content, and build reputation through on-chain engagement.

## Recent Changes

### 2025-10-04: User Profiles Feature
- Added editable user profiles with display names and avatars
- Profile pictures stored on IPFS via Web3.Storage
- Profile pages display user stats (reputation, likes, posts) and post history
- Usernames are clickable throughout the app and link to profile pages
- PostFeed displays author names and avatars when available
- Edit profile modal allows name changes and avatar uploads
- Cache invalidation ensures profile updates reflect across the entire app

### 2025-10-04: Reputation System Complete
- Fixed reputation calculation to use real on-chain data
- Rekeyed user storage by wallet address instead of UUID
- Users automatically created for all interactions
- Reputation updates correctly when receiving likes and tips
- Post validation prevents orphaned interactions
- All interaction endpoints ensure post existence before processing

## Project Architecture

### Tech Stack
- **Frontend**: React + Vite, TailwindCSS, shadcn/ui components
- **Backend**: Express.js with in-memory storage (MemStorage)
- **Blockchain**: HeLa blockchain with Solidity smart contracts
- **Storage**: IPFS via Web3.Storage for content and images
- **Wallet**: MetaMask integration with ethers.js

### Key Files
- `shared/schema.ts` - Drizzle schemas and Zod validation
- `server/storage.ts` - In-memory storage interface and implementation
- `server/routes.ts` - Express API endpoints
- `client/src/components/PostFeed.tsx` - Main feed component
- `client/src/pages/profile.tsx` - User profile page
- `client/src/lib/web3.ts` - Blockchain interaction utilities
- `client/src/lib/ipfs.ts` - IPFS upload functionality
- `contracts/SocialFeed.sol` - Smart contract for on-chain interactions

### Data Model
- **Users**: Stored by lowercase wallet address with name, avatar, reputation, totalLikes, totalTips
- **Posts**: Content hash, image hash, author address, engagement metrics
- **Comments**: Linked to posts via postId
- **Likes**: One per user per post
- **Tips**: HELA token transfers between users on posts

### Storage Architecture
- MemStorage uses Map<string, T> for each entity type
- Users keyed by lowercase wallet address (not UUID)
- Automatic user creation on first interaction
- Reputation calculated from likes and tips received

### API Endpoints
- `GET /api/posts` - Fetch posts with author enrichment (name, avatar, reputation)
- `POST /api/posts` - Create new post
- `POST /api/likes` - Like a post (validates post exists)
- `POST /api/comments` - Comment on post (validates post exists)
- `POST /api/tips` - Send HELA tip (validates post exists)
- `GET /api/users/:address` - Get user profile and their posts
- `PATCH /api/users/:address` - Update user profile (name, avatar)
- `GET /api/stats` - Platform statistics

### Frontend Routes
- `/` - Home page with post feed and create post form
- `/profile/:address` - User profile page

## User Preferences

*None specified yet*

## Environment Setup

### Required Secrets
- `VITE_WEB3_STORAGE_TOKEN` - Web3.Storage API token for IPFS uploads (required for posting with images and avatar uploads)
- `SESSION_SECRET` - Express session secret (auto-configured)

### Development
```bash
npm run dev  # Starts Express + Vite dev server on port 5000
```

## Features

### Implemented
- ✅ MetaMask wallet connection
- ✅ Create posts with text and images (IPFS)
- ✅ Like posts (on-chain)
- ✅ Comment on posts (on-chain)
- ✅ Tip posts with HELA tokens (on-chain)
- ✅ Real-time reputation system
- ✅ User profiles with editable names and avatars
- ✅ Profile pages with post history and stats
- ✅ Clickable usernames throughout the app

### Planned
- ⏳ Post filtering by author
- ⏳ Trending posts algorithm
- ⏳ Notification system for interactions
- ⏳ Leaderboard showing top users
- ⏳ Post editing and deletion with on-chain history

## Design

### Theme
- Modern glassmorphism aesthetic
- Green (#10b981) and black color scheme
- Gradient accents and blur effects
- Dark mode optimized

### UI Components
- shadcn/ui component library
- Lucide React icons
- Tailwind CSS for styling
- Responsive design
