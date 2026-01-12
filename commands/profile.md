---
description: Switch iTerm2 session to a different profile
argument-hint: PROFILE_NAME
allowed-tools: [Bash]
---

# Switch iTerm2 Profile

Apply a different iTerm2 profile to the current session. This changes the colors, fonts, and other settings defined in the profile.

## Arguments

- `PROFILE_NAME`: The name of the iTerm2 profile to apply

## Instructions

1. Get the profile name from the argument.

2. Execute AppleScript to set the profile on the current session.

3. Do NOT output any commentary - just execute the AppleScript silently.

## AppleScript Reference

```applescript
-- Set profile on current session
tell application "iTerm2"
  tell current session of current tab of current window
    set profile name to "ProfileName"
  end tell
end tell
```

## Notes

- Profile names are case-sensitive and must match exactly
- Available profiles can be found in iTerm2 Preferences > Profiles
- Common default profiles: "Default", "Hotkey Window"
