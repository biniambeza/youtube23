# Frontend Client - Fiverr Clone

Frontend Single Page Application built with **React 18**, **Vite**, and **SCSS**, communicating with the backend API via Axios and TanStack Query.

## Scripts

```bash
npm install     # Install dependencies
npm run dev     # Start development server
npm run build   # Build production bundle
npm run preview # Preview production build locally
```

## Environment Variables (`.env`)

```env
VITE_UPLOAD_LINK=https://api.cloudinary.com/v1_1/<cloud_name>/image/upload
```

## Features

- **React 18 & Vite**: Fast HMR and bundle optimization.
- **TanStack React Query**: Efficient data fetching, caching, and cache invalidation.
- **Stripe Elements**: In-app secure card payments.
- **SCSS**: Modular, component-scoped styles.
- **Pages**:
  - `home`: Hero section, featured services, trusted brands, category slides
  - `gigs`: Service catalog with filtering by price, sorting, and category
  - `gig`: Detailed view with seller bio, pricing tiers, and reviews
  - `add`: Gig creation form (for seller accounts)
  - `orders`: Overview of purchased/sold gigs
  - `myGigs`: Management view for seller's own listings
  - `messages` & `message`: Real-time inbox and chat threads
  - `pay` & `success`: Stripe checkout and order confirmation
