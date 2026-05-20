# Dark Phoenix Assignment Write-Up

## Overview

This is the write-up for the **Dark Phoenix** Assignment for Lunartech. It will discuss the following:

- What changed from the original repository?
- Why the chosen stack was selected?
- How YouTube ingestion is wired into the existing S3/Modal flow?
- How is watermarking implemented?
- What failed during deployment and what were the fixes?
- What would I improve with another week?

This document will be updated throughout the week-long development cycle.

## Table of Contents

- [What Changed](#what-changed)
- [Deployment Stack](#deployment-stack)
- [YouTube Ingestion](#youtube-ingestion)
- [Watermarking Implementation](#watermarking-implementation)
- [What Failed During Deployment + Fixes](#what-failed-during-deployment--fixes)
- [What I Would Improve](#what-i-would-improve)

## What Changed

### Frontend Changes

1. Addition of `.npmrc` file in the frontend directory to fix `npm install` failure. Necessary due to a peer-dependency mismatch with `shadcn-dropzone@0.2.1` and `react@^18`.

### Backend Changes

1. Wrapped heavy runtime imports (whisperx, cv2, boto3, etc.) in `with image.imports():` so they only execute inside Modal's container, not locally during `modal deploy`'s file-discovery import. Avoids needing the full ML stack on the dev machine, including `torch==2.0.1`, which doesn't build on Python 3.12.

2. Added a pre-install step to the Modal image and passed `extra_options="--no-build-isolation"` to `pip_install_from_requirements`. The pinned older ML packages don't declare their build-time dependencies in `pyproject.toml`, so modern pip's isolated build environment couldn't resolve them.

## Deployment Stack

## YouTube Ingestion

## Watermarking Implementation

## What Failed During Deployment + Fixes

1. Peer-dependency conflict --> Created `.npmrc`

2. Heavy runtime imports in `main.py` (boto3, cv2, whisperx, etc.) broke `modal deploy` locally, as module-level imports get executed during file discovery, and `whisperx`/`torch==2.0.1` can't be installed on Python 3.12 --> `image.imports()` refactor in `main.py`

3. Prisma CLI couldn't find `DATABASE_URL` (`.env` is at the root, Prisma reads CWD) --> Sourced `.env` into the shell before `npm run db:push`

4. Modal container build failed on whisperx (`pkg_resources` and `Cython` were missing) --> Pre-installed build tools in the image [See Backend Changes](#backend-changes)

## What I Would Improve
