# Dark Phoenix Deployment Documentation

## Overview

This is the deployment documentation and guide for **Dark Phoenix**.

## Deployed URLs

- Frontend: TODO
- Backend Modal endpoint: <https://mvttjb--ai-podcast-clipper-aipodcastclipper-process-video.modal.run>

## Stack

- Frontend Hosting: Vercel
- Database: Supabase Postgres
- Object Storage: AWS S3 (Region: us-east-2, Bucket Name: dark-phoenix-mvttjb)
- Workflow Queue: Inngest Cloud
- GPU Backend: Modal
- AI Analysis: Google Gemini

## Environment Variables

| Variable | Used By | Notes |
| --- | --- | --- |
| DATABASE_URL | Frontend | Supabase pooler URL on Vercel, direct URL locally |
| AWS_ACCESS_KEY_ID | Frontend, Backend | IAM user with s3:GetObject/PutObject |
| AWS_SECRET_ACCESS_KEY | Frontend, Backend | Paired with AWS_ACCESS_KEY_ID, same IAM user |
| AWS_REGION | Frontend, Backend | us-east-2 |
| S3_BUCKET_NAME | Frontend, Backend | dark-phoenix-mvttjb |
| PROCESS_VIDEO_ENDPOINT | Frontend | <https://mvttjb--ai-podcast-clipper-aipodcastclipper-process-video.modal.run> |
| PROCESS_VIDEO_ENDPOINT_AUTH | Frontend | Matches Modal's AUTH_TOKEN |
| GEMINI_API_KEY | Backend (Modal secret) | Generated at aistudio.google.com/app/apikey |
| AUTH_TOKEN | Backend (Modal secret) | Same value as PROCESS_VIDEO_ENDPOINT_AUTH |
| BASE_URL | Frontend | Vercel deployment URL |
| AUTH_SECRET | Frontend | next-auth |
| STRIPE_* | Frontend | Test mode |

## Inngest Configuration

TODO

## Reviewer Access

TODO

## How to Reproduce the Assigned Video Job

TODO

## Watermark Implementation

TODO

## Finding Generated Clips

TODO

## How to Regenerate and Re-upload the Clips

TODO

## Known Limitations

TODO
