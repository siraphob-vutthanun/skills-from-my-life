---
name: youtube-status-official-api
description: Use when checking, implementing, reviewing, or debugging YouTube channel status, live status, upload status, video ownership, or notification eligibility. Requires official YouTube Data API v3 endpoints only and forbids HTML scraping, /live page inspection, redirect parsing, canonical URL parsing, or regex extraction from YouTube pages.
---

# YouTube Status via Official API

Use this skill whenever an agent needs to decide whether a YouTube channel is live, whether a video belongs to a channel, or whether a Discord notification is eligible.

## Hard Rule

Use the official YouTube Data API v3 as the source of truth. Do not inspect, scrape, regex, or parse YouTube HTML pages for:

- live status
- channel ownership
- `videoId` discovery
- redirect targets
- canonical URLs
- watch page metadata
- `/channel/.../live` or `/@handle/live` output

HTML fallback is forbidden for status decisions, even if a later API call would verify the candidate. A bad HTML candidate can still create noisy logs, poisoned state, wasted quota, and false debugging trails.

If the API cannot answer the question because the key is invalid, quota is exhausted, the response is empty, or the endpoint fails, fail closed and do not send.

## Active Live Flow

To discover whether a configured channel is currently live:

1. Read the configured `channelId`.
2. Call YouTube Data API v3 `search.list` with:
   - `part=snippet`
   - `channelId=<configured channel id>`
   - `type=video`
   - `eventType=live`
   - `order=date`
   - a small `maxResults`
3. For each returned `videoId`, call `videos.list` with:
   - `part=snippet,liveStreamingDetails`
   - `id=<video id>`
4. Notify only when all of these are true:
   - `snippet.channelId` equals the configured channel id
   - `liveStreamingDetails.actualStartTime` is present
   - `liveStreamingDetails.actualEndTime` is absent
   - the video id is not already in durable notification state

Do not use YouTube web URLs to discover the current live video.

## Video and Upload Verification

For a known video id, call `videos.list` and require:

- `snippet.channelId` equals the configured channel id
- `snippet.title` is present for notification text
- `snippet.liveBroadcastContent` and `liveStreamingDetails` are interpreted consistently with the requested status

Completed live archives are not ordinary uploads unless the product explicitly asks to notify completed live archives.

## Debugging Checklist

When debugging a missed or skipped notification, report API evidence rather than page evidence:

- exact endpoint family used: `search.list` or `videos.list`
- whether the API key was accepted
- returned `videoId` values, if any
- returned `snippet.channelId`
- returned `snippet.liveBroadcastContent`
- returned `liveStreamingDetails.actualStartTime`
- returned `liveStreamingDetails.actualEndTime`
- relevant remote durable state, such as notified ids and last live id

Never explain YouTube status from `/live` HTML, page canonical URLs, redirects, or global `isLive` markers.

## Official References

- https://developers.google.com/youtube/v3/docs/search/list
- https://developers.google.com/youtube/v3/docs/videos/list
- https://developers.google.com/youtube/v3/docs/videos
