# Personal Blog Platform

A modern, feature-rich blog platform built with Next.js 14, focusing on book reviews, movie reviews, and personal learnings.

## Features

- 📝 Rich Text Editor for blog posts
- 🖼️ Image upload and management
- 🎥 YouTube video embedding
- 🏷️ Category-based organization
- 🎨 Responsive, modern design
- 🔍 Search functionality
- 🏷️ Tag-based filtering
- 📱 Mobile-friendly interface
- 🌓 Dark/Light mode

## Tech Stack

- **Frontend:**
  - Next.js 14 (App Router)
  - TypeScript
  - Tailwind CSS
  - Shadcn/ui Components
  - TipTap Editor
  - React Query

- **Backend:**
  - Next.js API Routes
  - Prisma ORM
  - PostgreSQL
  - Cloudinary (Image Storage)

- **Authentication:**
  - NextAuth.js
  - GitHub OAuth

- **Deployment:**
  - Vercel
  - Railway (PostgreSQL)

## Project Structure

```
blog-platform/
├── app/
│   ├── (auth)/
│   │   ├── login/
│   │   └── register/
│   ├── (blog)/
│   │   ├── [slug]/
│   │   ├── category/[category]/
│   │   └── tag/[tag]/
│   ├── api/
│   │   ├── auth/
│   │   ├── posts/
│   │   └── upload/
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── blog/
│   │   ├── BlogCard.tsx
│   │   ├── BlogEditor.tsx
│   │   └── BlogList.tsx
│   ├── common/
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   └── Layout.tsx
│   └── ui/
│       ├── Button.tsx
│       └── Modal.tsx
├── lib/
│   ├── prisma.ts
│   ├── auth.ts
│   └── utils.ts
├── prisma/
│   └── schema.prisma
├── public/
├── styles/
│   └── globals.css
├── types/
│   └── index.ts
├── .env.example
├── package.json
└── tsconfig.json
```

## Database Schema

```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String?
  image     String?
  posts     Post[]
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Post {
  id          String      @id @default(cuid())
  title       String
  slug        String      @unique
  content     String      @db.Text
  coverImage  String?
  published   Boolean     @default(false)
  category    Category    @relation(fields: [categoryId], references: [id])
  categoryId  String
  tags        Tag[]
  author      User        @relation(fields: [authorId], references: [id])
  authorId    String
  createdAt   DateTime    @default(now())
  updatedAt   DateTime    @updatedAt
}

model Category {
  id          String    @id @default(cuid())
  name        String    @unique
  description String?
  posts       Post[]
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
}

model Tag {
  id        String   @id @default(cuid())
  name      String   @unique
  posts     Post[]
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/blog-platform.git
cd blog-platform
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
```

4. Update `.env` with your credentials:
```env
DATABASE_URL="postgresql://user:password@localhost:5432/blog"
NEXTAUTH_SECRET="your-secret-key"
NEXTAUTH_URL="http://localhost:3000"
CLOUDINARY_CLOUD_NAME="your-cloud-name"
CLOUDINARY_API_KEY="your-api-key"
CLOUDINARY_API_SECRET="your-api-secret"
```

5. Initialize database:
```bash
npx prisma db push
```

6. Run the development server:
```bash
npm run dev
```

## Main Features Implementation

### 1. Blog Editor Modal
- Uses a modal component from shadcn/ui
- Implements TipTap for rich text editing
- Supports image upload to Cloudinary
- YouTube video embedding support
- Category and tag selection

### 2. Post Categories
- Book Reviews
- Movie Reviews
- YouTube Videos
- Personal Learnings
- Tech Articles

### 3. Post Features
- Rich text content
- Cover image
- Embedded YouTube videos
- Category assignment
- Multiple tags
- Author information
- Reading time estimate

## Deployment

1. Create a new project on Vercel
2. Connect your GitHub repository
3. Set up environment variables in Vercel
4. Deploy!

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.