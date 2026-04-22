---
name: deploy
description: Deploys this Next.js issue tracker app. Use when the user wants to build, run locally, or deploy with Docker. Supports "local", "docker", "docker-local" as arguments.
---

# Deploy Skill

This skill handles the deployment workflow for the Next.js issue tracker. The workflow varies based on the target environment.

## Arguments

- `local` — Build and run locally for final verification
- `docker` — Build Docker image and run container
- `docker-local` — Build and run Docker container locally (same as `docker`)

## Workflow

### Always: Pre-deploy checks

Before any deployment, verify the build compiles successfully:

```bash
bun run build
```

If the build fails, fix the errors first. Never deploy a broken build.

### Local deployment (without Docker)

When the user specifies `local`:

1. Run `bun run build` to create a production build
2. Start the production server with `bun run start`
3. Tell the user the app is running at http://localhost:3000

Note: The dev server (`bun run dev`) is NOT a deployment — it's for development with hot reload. The local deployment here verifies the production build works correctly.

### Docker deployment

When the user specifies `docker` or `docker-local`:

1. **Verify prerequisites:**
   - Check Docker is installed: `docker --version`
   - If not installed, tell the user to install Docker Desktop

2. **Build the image:**
   ```bash
   docker build -t issue-tracker .
   ```

3. **Run the container:**
   ```bash
   docker run -p 3000:3000 --name issue-tracker issue-tracker
   ```

4. **Tell the user:**
   - The app is running at http://localhost:3000
   - To stop: `docker stop issue-tracker`
   - To remove: `docker rm issue-tracker`
   - To rebuild after changes: `docker build -t issue-tracker .` (image name must match)

## Post-deployment

After any successful deployment, remind the user to:
- Verify the app loads correctly at http://localhost:3000
- Check that API routes respond (`GET /api/issues`)
- Monitor for any runtime errors in the terminal/container logs
