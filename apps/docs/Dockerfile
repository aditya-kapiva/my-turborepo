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

# Copy built files from builder stage
# Next.js standalone output or .next directory
COPY --from=builder --chown=nextjs:nodejs /app/.next ./.next
COPY --from=builder --chown=nextjs:nodejs /app/public ./public

# Copy other necessary files
COPY --from=builder --chown=nextjs:nodejs /app/next.config.js ./
COPY --from=builder --chown=nextjs:nodejs /app/package.json ./

USER nextjs

# Expose port
EXPOSE 8080

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD node -e "require('http').get('http://localhost:3001/', (r) => {process.exit(r.statusCode === 200 ? 0 : 1)})"

# Start the application
CMD ["npm", "start"]

