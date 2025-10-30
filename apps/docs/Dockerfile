# Build stage
FROM node:22-alpine AS builder

WORKDIR /app

# Copy package files
COPY package.json package-lock.json* ./

# Install dependencies
RUN npm i

# Copy source files
COPY . .

# Build Next.js application
RUN npm run build

# Production stage
FROM node:22-alpine AS production

WORKDIR /app

# Set environment to production
ENV NODE_ENV=production

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nextjs -u 1001

# Copy package files
COPY package.json package-lock.json* ./

# Install only production dependencies
RUN npm i --only=production && npm cache clean --force

# Copy ALL necessary files from builder stage
COPY --from=builder --chown=nextjs:nodejs /app/.next ./.next
COPY --from=builder --chown=nextjs:nodejs /app/public ./public
COPY --from=builder --chown=nextjs:nodejs /app/next.config.js ./
COPY --from=builder --chown=nextjs:nodejs /app/package.json ./
COPY --from=builder --chown=nextjs:nodejs /app/node_modules ./node_modules

# If using App Router, ensure app directory is copied
COPY --from=builder --chown=nextjs:nodejs /app/app ./app/

# If using Pages Router, ensure pages directory is copied  
COPY --from=builder --chown=nextjs:nodejs /app/pages ./pages/

# Copy any other necessary files
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static

USER nextjs

# Expose port (Cloud Run uses 8080 by default)
EXPOSE 8080

# Health check - FIXED port to match your app
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD node -e "require('http').get('http://localhost:8080/', (r) => {process.exit(r.statusCode === 200 ? 0 : 1)})"

# Start the application on port 8080
CMD ["npm", "start"]