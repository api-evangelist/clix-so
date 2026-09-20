---
name: Clix
description: Use when building mobile push notification systems, managing user engagement campaigns, triggering transactional messages, tracking user events, or integrating push notifications into iOS, Android, React Native, or Flutter applications. Reach for this skill when working with campaign creation, API-triggered messaging, user segmentation, personalization, or debugging notification delivery issues.
metadata:
    mintlify-proj: clix
    version: "1.0"
---

# Clix Skill

## Product Summary

Clix is a mobile push notification platform that enables developers to send, manage, and track push notifications across iOS, Android, React Native, and Flutter applications. Agents use Clix to create campaigns, trigger messages via API, manage users, track events, and personalize content. The primary documentation is at https://docs.clix.so. Key tools include the Clix CLI (`clix` command), REST API endpoints at `https://api.clix.so`, SDKs for each platform, and the Clix MCP Server for AI agent integration. Configuration uses project IDs and API keys (public for client-side, secret for backend).

## When to Use

Reach for this skill when:
- **Building notification systems**: Setting up push notifications in mobile apps (iOS, Android, React Native, Flutter)
- **Creating campaigns**: Designing scheduled, event-triggered, or API-triggered messaging campaigns in the Clix console
- **Triggering messages from backend**: Calling API endpoints to send transactional alerts, workflow notifications, or system messages
- **Managing users**: Creating, updating, or deleting users; setting user properties for segmentation
- **Tracking events**: Instrumenting apps to capture user actions that drive campaign triggers or personalization
- **Personalizing content**: Using template syntax to insert dynamic user data, event properties, or API-provided values into messages
- **Debugging delivery**: Troubleshooting why notifications aren't reaching devices or aren't being sent
- **Setting up SDKs**: Installing and configuring Clix SDKs in mobile projects using the CLI or manual setup
- **Integrating with AI agents**: Using the Clix MCP Server to enable Claude, Cursor, or other agents to access Clix docs and SDK examples

## Quick Reference

### Essential CLI Commands

| Command | Purpose |
|---------|---------|
| `clix install` | Auto-configure push notifications; prepares project then hands off to AI agent |
| `clix doctor` | Diagnose SDK integration status and configuration completeness |
| `clix login` | Authenticate with Clix account via device flow |
| `clix mcp` | Install Clix MCP Server for AI agent integration |
| `clix skills` | Install Clix Skills for pre-built workflows |
| `clix agent [name]` | List or switch between supported AI agents |
| `clix update` | Check for and apply CLI updates |

### API Authentication Headers (Required for All Requests)

```
X-Clix-Project-ID: your_project_id
X-Clix-API-Key: your_api_key (secret key for backend, public key for SDKs)
Content-Type: application/json
```

### Core API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/users` | POST | Create a new user |
| `/api/v1/users/{user_id}` | PATCH | Update user properties |
| `/api/v1/users/{user_id}` | DELETE | Delete a user |
| `/api/v1/campaigns/{campaign_id}:trigger` | POST | Trigger an API-triggered campaign |
| `/api/v1/messages:send` | POST | Send ad-hoc push notifications |
| `/api/v1/live-activities:start` | POST | Start iOS Live Activities |

### Campaign Types

| Type | When to Use | Trigger |
|------|-------------|---------|
| **Scheduled** | Promotions, digests, announcements | Fixed time (once, daily, recurring) |
| **Event-triggered** | Confirmations, onboarding, reviews | User action (e.g., purchase_completed) |
| **API-triggered** | System alerts, workflows, transactional | Backend API call with dynamic data |

### User Types

| Type | Identification | Use Case |
|------|---|---|
| **Identified User** | Has `project_user_id` (your system ID) | Logged-in users; enables consistent tracking |
| **Anonymous User** | No `project_user_id`; has auto-generated `anonymous_id` | Pre-login browsing; temporary sessions |

### Personalization Syntax

| Namespace | Example | Use |
|-----------|---------|-----|
| `user.*` | `{{ user.username }}`, `{{ user.tier }}` | User properties |
| `event.*` | `{{ event.distance }}`, `{{ event.name }}` | Event properties |
| `trigger.*` | `{{ trigger.order_id }}`, `{{ trigger.discount }}` | API payload data |
| `device.*` | `{{ device.platform }}`, `{{ device.locale }}` | Device info (IOS, ANDROID, locale, timezone) |

### Rate Limits

- **Management Operations**: 1,000 requests per second
- **Includes**: User management, message sending, campaign triggering
- **Response on limit**: HTTP 429 (Too Many Requests)
- **Headers**: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`

## Decision Guidance

### When to Use Campaign Type

| Scenario | Use This | Why |
|----------|----------|-----|
| Send at a specific time (e.g., 10 AM daily) | Scheduled | Time-based delivery is built-in |
| Notify when user completes an action | Event-triggered | Automatic trigger on event; no backend call needed |
| Send transactional alert from backend | API-triggered | Backend controls when; console controls message/audience |
| Need dynamic content from backend | API-triggered | Pass properties via API; use `trigger.*` in template |
| Complex filtering logic | API-triggered (with backend logic) | Keep audience filters simple (max 3 attributes); move complex logic to backend |

### When to Use API Key Type

| Scenario | Use This | Why |
|----------|----------|-----|
| Client-side SDK (mobile app) | Public API Key | Safe to expose; SDKs handle token registration |
| Backend service (user management, triggering) | Secret API Key | Confidential; never expose in client code |
| Testing locally | Secret API Key | Full access for development |

### When to Use User Management

| Scenario | Action | Why |
|----------|--------|-----|
| App starts, user not logged in | Do nothing (anonymous by default) | Clix auto-assigns anonymous profile |
| User logs in | Call `setUserId("user_id")` | Converts anonymous to identified; merges history |
| User logs out | Do nothing (default) | Events still attributed to last known user |
| Shared device, need full reset | Call `reset()` then `initialize()` | Clears device ID; next user appears as new anonymous |

## Workflow

### 1. Set Up SDK in Mobile Project

1. **Install CLI**: `npm install -g @clix-so/clix-cli` or use homebrew/curl
2. **Authenticate**: `clix login`
3. **Run install**: `clix install` (prepares Firebase/APNs, hands off to AI agent for SDK setup)
4. **Verify**: `clix doctor` (checks configuration completeness)
5. **Test**: Send a test message from Clix console to confirm delivery

### 2. Create and Launch a Campaign

1. **Open Clix console** and go to Campaigns > Create Campaign
2. **Choose type**: Scheduled, Event-triggered, or API-triggered
3. **Configure message**: Title, body, image URL, deep link
4. **Set audience**: Add filters (user properties, device attributes)
5. **For API-triggered**: Select "API-triggered" in Schedule step; save to get campaign ID
6. **Launch**: Review summary and click Launch
7. **Monitor**: Track Targeted, Sent, Delivered, Tapped metrics

### 3. Trigger Campaign from Backend (API-Triggered)

1. **Get campaign ID** from console (visible in URL or campaign details)
2. **Prepare payload** with audience and properties:
   ```json
   {
     "audience": { "broadcast": true },
     "properties": { "order_id": "123", "customer_name": "Alice" }
   }
   ```
3. **Call trigger endpoint**:
   ```bash
   POST https://api.clix.so/api/v1/campaigns/{campaign_id}:trigger
   Headers: X-Clix-Project-ID, X-Clix-API-Key, Content-Type: application/json
   Body: { "audience": {...}, "properties": {...} }
   ```
4. **Handle response**: Check for `trigger_id` (success) or error message
5. **Implement retry logic**: Use exponential backoff for 5xx errors; respect 429 rate limits

### 4. Track Events in App

1. **Identify user action** to track (e.g., "purchase_completed")
2. **Call SDK method** with event name and properties:
   ```swift
   Clix.trackEvent("purchase_completed", properties: ["amount": 99.99, "product": "shoes"])
   ```
3. **Use in campaigns**: Reference `event.*` in event-triggered campaign filters and personalization
4. **Handle errors**: Wrap in try-catch; log failures for debugging

### 5. Personalize Message Content

1. **Identify data sources**: User properties, event properties, or API trigger data
2. **Use template syntax** in message title/body:
   ```
   Hi {{ user.username }}, your order #{{ trigger.order_id }} is ready!
   ```
3. **Add conditionals** for branching:
   ```liquid
   {% if user.tier == "premium" %}
   Exclusive offer: 20% off
   {% else %}
   Standard offer: 10% off
   {% endif %}
   ```
4. **Test with preview**: Use campaign preview to verify personalization before launch
5. **Use filters** for missing data: `{{ user.discount | default: "10%" }}`

## Common Gotchas

- **Missing Firebase setup**: Clix requires Firebase (FCM for Android, APNs for iOS). Run `clix install` to auto-configure.
- **Permissions not granted**: Users must grant notification permissions in device settings. Check Clix dashboard device list to confirm permission status.
- **Outdated Xcode/simulator**: iOS notifications won't work on old Xcode or simulator versions. Update both.
- **Cold boot required for Android emulator**: Emulator must start with cold boot, not warm boot. Set in Device Manager > Additional Settings.
- **Event names must match exactly**: Event-triggered campaigns only fire on new events matching the exact name and properties. Historic events are not replayed.
- **Audience filter limit**: Maximum 3 attributes per audience definition. Move complex logic to backend before calling trigger API.
- **Rate limit 429 errors**: Implement exponential backoff; monitor `X-RateLimit-Remaining` header to avoid hitting limit.
- **API key exposure**: Never commit secret API keys to version control. Use environment variables or secrets management.
- **User merge on login**: When `setUserId()` is called on an anonymous user, Clix merges history if identifiable attributes match. Ensure consistent user IDs.
- **Reset clears device ID**: Calling `reset()` generates a new device ID. Use only for shared devices or full anonymization.
- **Template rendering errors**: Unknown variables render as empty string; invalid conditions evaluate to false. Check Message Logs for errors.
- **Deprecated `removeUserId()`**: Use `reset()` instead for logout/anonymization.

## Verification Checklist

Before submitting work with Clix:

- [ ] **SDK installed**: Run `clix doctor` and confirm no errors
- [ ] **Firebase configured**: APNs certificate (iOS) and FCM key (Android) are set up
- [ ] **User identification**: Identified users have `project_user_id`; anonymous users have `anonymous_id`
- [ ] **Permissions granted**: Test device has notification permissions enabled (Settings > Notifications)
- [ ] **Event tracking**: Events are being captured with correct names and properties (check dashboard)
- [ ] **Campaign audience**: Audience filters are correct and estimate matches expected user count
- [ ] **Personalization**: Message preview shows correct variable substitution; no empty or malformed values
- [ ] **API authentication**: Headers include valid `X-Clix-Project-ID` and `X-Clix-API-Key`
- [ ] **Rate limit handling**: Retry logic implements exponential backoff for 5xx and 429 errors
- [ ] **Test message sent**: Send test from console to confirm delivery to device
- [ ] **Deep links work**: If using deep links, verify they open correct app screen
- [ ] **Error handling**: All API calls have try-catch or error callbacks

## Resources

- **Comprehensive navigation**: https://docs.clix.so/llms.txt (page-by-page listing for agent reference)
- **API Reference**: https://docs.clix.so/api-reference/overview (authentication, endpoints, rate limits, error handling)
- **Campaign Setup**: https://docs.clix.so/campaigns/api-triggered (API-triggered campaigns, dynamic filtering, personalization examples)
- **Clix CLI**: https://docs.clix.so/clix-cli (installation, commands, agent support)

---

> For additional documentation and navigation, see: https://docs.clix.so/llms.txt