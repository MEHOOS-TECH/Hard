# Venx Upload

A minimalist Google-style file upload app built with Next.js, React, TailwindCSS, and Supabase Storage.

## Features

- 📱 **Mobile-first** — tap card to open phone gallery/file picker
- 🖱️ **Drag & drop** — drag files from desktop
- ⚡ **Instant uploads** — real-time progress bars with animations
- 🖼️ **Rich previews** — images, video, and audio preview inline
- 🔗 **Quick actions** — open, copy link, or download after upload
- 🎨 **Google-inspired UI** — clean white card design with smooth animations
- 📁 **All file types** — images, video, audio, PDF, ZIP, Word, Excel, and more

## Folder Structure

```
venx-upload/
├── src/
│   ├── app/
│   │   ├── globals.css        # Tailwind + Google fonts + animations
│   │   ├── layout.tsx         # Root layout with metadata
│   │   └── page.tsx           # Main page
│   ├── components/
│   │   ├── UploadZone.tsx     # Core upload logic + drag/drop
│   │   ├── UploadProgressCard.tsx  # In-progress file card
│   │   ├── UploadedFileCard.tsx    # Completed file with preview
│   │   └── FileIcon.tsx       # Color-coded file type icons
│   └── lib/
│       ├── supabase.ts        # Supabase client + helpers
│       └── fileUtils.ts       # Types, MIME utils, formatters
├── .env.local                 # Local environment variables
├── .env.example               # Template for deployment
├── next.config.js             # Next.js + image domain config
├── tailwind.config.ts         # TailwindCSS configuration
├── tsconfig.json
└── package.json
```

## Quick Start

### 1. Install dependencies

```bash
npm install
```

### 2. Set environment variables

Copy `.env.example` to `.env.local` and fill in your Supabase credentials:

```bash
cp .env.example .env.local
```

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

### 3. Run development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### 4. Build for production

```bash
npm run build
npm start
```

---

## Supabase Setup

### Storage bucket

1. Go to your [Supabase dashboard](https://app.supabase.com)
2. Navigate to **Storage**
3. Create a bucket named `venx`
4. Set it to **Public** (so uploaded files can be accessed via URL)

### Bucket policy (public read)

In the SQL editor, run:

```sql
-- Allow anyone to read files
CREATE POLICY "Public read" ON storage.objects
  FOR SELECT USING (bucket_id = 'venx');

-- Allow anyone to upload files
CREATE POLICY "Public upload" ON storage.objects
  FOR INSERT WITH CHECK (bucket_id = 'venx');
```

---

## Deploy to Vercel

### Option A: Vercel CLI

```bash
npm i -g vercel
vercel
```

Follow the prompts. When asked for environment variables, add:
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

### Option B: GitHub + Vercel Dashboard

1. Push this project to a GitHub repo
2. Go to [vercel.com/new](https://vercel.com/new)
3. Import your repository
4. Under **Environment Variables**, add:
   - `NEXT_PUBLIC_SUPABASE_URL` = your Supabase project URL
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY` = your Supabase anon key
5. Click **Deploy**

---

## Tech Stack

| Tool | Version | Purpose |
|------|---------|---------|
| Next.js | 14.x | React framework with App Router |
| React | 18.x | UI library |
| TailwindCSS | 3.x | Utility-first styling |
| @supabase/supabase-js | 2.x | Supabase Storage SDK |
| Google Sans | — | Typography |

---

## Customization

### Change the bucket name
Update `BUCKET` in `src/lib/supabase.ts`:
```ts
export const BUCKET = "your-bucket-name";
```

### Restrict file types
Edit `ACCEPTED_TYPES` in `src/lib/fileUtils.ts`

### Change upload folder
Edit `generateFilePath()` in `src/lib/fileUtils.ts`
